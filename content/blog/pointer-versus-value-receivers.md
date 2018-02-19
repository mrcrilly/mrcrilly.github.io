---
title: "Pointer versus Value Receivers in Go"
date: 2018-02-20T08:30:00+00:00
---

Just a brief note: it's important to know the difference between a pointer and a value based reciver on a `struct{}` in Go. By "value based" I mean not working with a pointer on the receiver, which means the receiving function gets everything as a value. Why is this important? Example time...

## Hello, World 42!
Check out this basic, silly `struct{}`:

```go
type Data struct {
	A string
	B string
	C uint
}

func (d Data) SetA(newA string) {
	d.A = newA
}
```

Nothing special here at all. Let's use it in `main()`:

```go
func main() {
	data := Data{A: "Hello", B: "World", C: 42}
	fmt.Printf("%+v\n", data)

	data.SetA("Goodbye")
	fmt.Printf("%+v\n", data)
}
```

What's the output of both `Printf()` statments? What we should see is `{A:Hello B:World C:42}` followed by `{A:Goodbye B:World C:42}`, but we don't...

```go
{A:Hello B:World C:42}
{A:Hello B:World C:42}
```

Eh? But we changed `A`? No we didn't. **Go passes everything by value, even pointers, and even to receivers.** We have to ignore common OOP principles which tell us that `SetA()` on our type is a method, when it's not, at least not in the traditional OOP sense.

In short what's happening here is Go is sending the receiver a copy of `data`. Because our receiver is getting a copy, any changes to the fields on that copy aren't reflected in our original `data` variable. When you know Go passes everything by value, as a copy, even to receivers, it become sobvious what the solution is. Let's fix our code...

```go
// ...

func (d *Data) SetA(newA string) {
	d.A = newA
}
```

Same structure but we've changed the `SetA()` receiver to a pointer receiver, which means Go will send a pointer to the original variable, `data`, instead of a copy... except it won't. **It'll send another copy**, but it is a copy of a **pointer** , and so the address the pointer is looking at is the original `data` variable, so we can make changes and get the results we expect:

```go
{A:Hello B:World C:42}
{A:Goodbye B:World C:42}
```

The `main()` function didn't have to be changed at all. It stayed the same, but the results are what we expected in the first place.

## When to use pointers
You can mix and match pointer and value based recievers as you see fit. The reasons for this aren't completely obvious, but getting to the point: you use a pointer based receiver when you need to manipulate fields on the "instance" of the structure, and a value based receiver when you want to simply work with the data in a static way (such as sending it to a remote API, or returning some other value not stored as a field.)

Here's an example of adding another receiver that's (rightly) value based:

```go
// ...

func (d Data) MutateC() uint {
	return d.C * 10
}
```

We're using the field `C` to return a new value. We're not storing the result of the calculation in the structure, so we don't need a pointer based receiver (nor should you use one, for fear of some side effect incorrectly manipulating the structure.) Here it is in use, for completeness:

```go
func main() {
	data := Data{A: "Hello", B: "World", C: 42}
	fmt.Printf("%+v\n", data)

	data.SetA("Goodbye")
	fmt.Printf("%+v\n", data)

	D := data.MutateC()
	fmt.Println(D)
}
```

And the output should be obvious to all:

```go
{A:Hello B:World C:42}
{A:Goodbye B:World C:42}
420
```

Maybe the actual answer to the great question is 420? [Complete example code here](https://goplay.space/#UjpW-foT3eE).
