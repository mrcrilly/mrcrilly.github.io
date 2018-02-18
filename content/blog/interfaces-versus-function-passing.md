---
title: "Interfaces vs Straight Functions"
date: 2018-02-14T07:00:00+01:00
---

How should I pass around (functional) dependencies? Via an `interface` or `func` type? I have an example to show why I will (mostly) always prefer interfaces.

## An Example
Let's review the following `struct{}`, which is going to hold the configuration for a completely the fictious application we'll be writing:

```go
type Configuration struct {
	MaxValue, MinValue  uint

	doubler doubleFunc
	tripler tripleFunc
}
```

It has four fields. The `MaxValue` and `MinValue` fields are somewhat self evident, but they're just used inside the `doubler()` and `tripler()` functions. Ignore them for now. The `func` fields, however, are what prompted me to write this brief article.

Recently I came across this very method of using functions as first-class citizens to allow table driven tests to override, or mock, the core functionality used by a (Go routine) worker. At first it seems to make sense, like if someone is explaining the theory to you, but when you see it in action you realise, or at least I realised, that this clearly a job for interfaces.

Let's look at the type definitions for these functions:

```go
type doubleFunc func(uint, uint, uint) uint
type tripleFunc func(uint, uint, uint) uint
```

Nothing unusual really. I've made these simple enough to make the example easy to follow. So how are these fields configured? Let's review part of our `main()` function

```go
func main() {
	if len(os.Args) <= 2 {
		fmt.Println("no args given: need min and max")
		return
	}

	c := Configuration{
		MinValue: func() uint {
			r, _ := strconv.Atoi(os.Args[1]) // 0 is current file
			return uint(r)
		}(),

		MaxValue: func() uint {
			r, _ := strconv.Atoi(os.Args[2])
			return uint(r)
		}(),
	}

	// ...
}
```

Somewhat standard stuff. Here we're using `os.Args` to take in two parameters from the CLI. It's not the ideal means of handling flags, the `flags` package is (at minimum; consider [Viper](https://github.com/spf13/viper) too), but this is a quick and dirty example. We're also setting the `MinValue` and `MaxValue` fields to some `uint` passed in on the CLI.

As a quick aside, we're using Lambdas in the `Configuration` initialisation so we can use `strconv.Atoi()` without having to deal with the returned `error` value or work with an external, temporary variable. This use of Lambdas is not to say that ignoring errors is good practice, but it speeds things along nicely for us here. Again, this is just an example.

So that's the configuration of our amazing application in place. Let's look at configuring those `function` types (inside `main()`):

```go
// ...
	doubler := concreteDoubler
	if c.doubler != nil {
		doubler = c.doubler
	}

	tripler := concreteTripler
	if c.tripler != nil {
		tripler = c.tripler
	}

	start(c, doubler, tripler)
// ...
```

(It doesn't actually matter what these two functions do, for the record.)

We can pass in override functions, say from within (table-driven) tests, and thus replace/mock the functions. So if the `function` fields in the configuration are `nil`, we assume there's no overrides and use our pre-defined implementations instead. The latter represents "production", I guess?

But there's something unusual with what we're doing here. Did you notice how the call to `start()` uses the `doubler` and `tripler` variables, which are of the type `func`, instead of using the fields, which can point to the same concrete implmentations, provided in the `Configuration` object? This is the setup I've been exposed to and asked to implement. It doesn't seem like it's idiomatic Go, even if it does work.

Let's keep going...

## Start()
If we look at the `start()` function we will see it's using the `Configuration` we've setup and also takes in the functions for performing the "maths":

```go
func start(c Configuration, d doubleFunc, t tripleFunc) {
	r := d(100, c.MinValue, c.MaxValue)
	if r == 0 {
		fmt.Println("Oh no! 100 didn't work!!")
	} else {
		fmt.Println("Maths has been done. We're good.")
	}

	r = t(5000, c.MinValue, c.MaxValue)
	if r == 0 {
		fmt.Println("Oh no! 5000 isn't enough!")
	} else {
		fmt.Println("Maths has been done. Good work!")
	}
}
```

An amazing feat of engineering.

What we're doing is using the functions passed to our `start()` function to do some fictional, pointless mathematics on static numbers. When I was told to implement things this way I questioned why we shouldn't simply use the `func` fields inside the `Configuration` object, like this:

```go
c.doubler(...)
c.tripler(...)
```

But this was rejected because it tightly coupled the functions to the `Configuration` object, which was an undesirable association. It gave the wrong impression that the functions belonged to the configuration and so on... OK.

Let's refine this down in a few steps.

## Start() v2
Let's begin by using the fields in the `Configuration` instead of these silly `func` variables we're handing around:

```go
func start(c Configuration) {
	r := c.doubler(100, c.MinValue, c.MaxValue)
	if r == 0 {
		fmt.Println("Oh no! 100 isn't enough!")
	} else {
		fmt.Println("Maths has been done")
	}

	r = c.tripler(5000, c.MinValue, c.MaxValue)
	if r == 0 {
		fmt.Println("Oh no! 5000 isn't enough!")
	} else {
		fmt.Println("Maths has been done")
	}
}
```

Three tiny changes:

- We've removed the additional function parameters from `starts()`'s signature
- We've made the call to `d()` become `c.doubler()`
- And we've made the call to `t()` become `c.tripler()`

The result is a cleaner function signature as well as a much easier to understand code base. Despite what was said about the use of using the function fields directly on the `Configuration` object, it's actually easier to trace back the functions to where they're coming from. Perhaps I'm expecting too much to think this is obvious.

## Defining the Override
Now when we're overriding we're not using variables to store the final function to be called and passing them around. Instead we check to see if the function has been provided and if not, we provide our own:

```go
if c.doubler == nil {
	c.doubler = concreteDoubler
}

if c.tripler == nil {
	c.tripler = concreteTripler
}
```

Much easier. This allows a caller to simply ignore the fields and trust that some default will be used.

But wait! There's more!

## Interfaces
Now let's do what you're supposed to do (if I may be so bold):

```go
type CoreConfiguration interface {
	doubler(uint) uint
	tripler(uint) uint
}

type Configuration struct{ MaxValue, MinValue uint }
func (c *Configuration) doubler(i uint) uint { return i * 2 }
func (c *Configuration) tripler(i uint) uint { return i * 3 }
```

So we have an interface and a concrete implementation of it. In my opinion, it's cleaner already. Let's keep going.

```go
func main() {
	if len(os.Args) <= 2 {
		fmt.Println("no args given: need min and max")
		return
	}

	c = &Configuration{
		MinValue: func() uint {
			r, _ := strconv.Atoi(os.Args[1]) // 0 is current file
			return uint(r)
		}(),

		MaxValue: func() uint {
			r, _ := strconv.Atoi(os.Args[2])
			return uint(r)
		}(),
	}

	start(c)
}
```

That is indeed the entire `main()` function, complete with configuration. No need to check for overrides and then set defaults when they're not present: it's a `struct{}` that complies with the `interface{}`. The rest you know: `start()` uses the functions (receivers) on the `Configuration` passed in. Let's override with an example:

```go
type MegaConfiguration struct { MinValue, MaxValue uint }
func (m *MegaConfiguration) doubler(i uint) uint {return i * m.MinValue }
func (m *MegaConfiguration) tripler(i uint) uint {return i * m.MaxValue }

func main() {
    	if len(os.Args) <= 2 {
		fmt.Println("no args given: need min and max")
		return
	}

	c = &MegaConfiguration{
		MinValue: func() uint {
			r, _ := strconv.Atoi(os.Args[1]) // 0 is current file
			return uint(r)
		}(),

		MaxValue: func() uint {
			r, _ := strconv.Atoi(os.Args[2])
			return uint(r)
		}(),
	}

	start(c)
}
```

It's so easy to override the functionality in this particular case it's silly. I'm all for interfaces in probably all cases and do not see the reasons behind using options one and two. This is just straight up easier to implement, understand, and is less cognitive overhead to work with.

What are your thoughts?
