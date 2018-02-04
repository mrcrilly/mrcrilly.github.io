---
title: "Go Testing: Moq and gotests"
date: 2018-02-04T00:40:17+01:00
draft: true
---

I recently getting more involved with writing tests at work. One thing I noticed with our code was a lot of function pointers in structs. When I queried what this was for I was told, "For mocking out the functions for easier testing." That's certainly one way to do it, but there's deffinitely a better way.

## Interfaces
Interfaces are one of Go's most underutilised features. They can be somewhat confusing and hard to get your head around, but when they're put in place they allow the above situation to be handled in a much more elegant manner. 

For those who are new to Go, let's define a quick interface so we have an example to work with throughout this article.

```
//go:generate moq -out user_mocks.go . userProfile
type userProfile interface {
	Name() string
	SetName(name string) bool

	Email() string
	SetEmail(email string) bool

	Password() string
	SetPassword(password string) bool

	SignedUp() time.Time
	SetSignedUp(date time.Time) bool
}
```

We'll get into the `//go:generate` line later.

This is a simple interface for a "user profile" type. We're saying any types that wish to implement the interface must conform to having these receivers. Pretty simple stuff, really. 

Nothing more to be said?

## An Implementation
Let's write a simple implementation for the interface above.

```
type profile struct {
	RealName       string
	EmailAddress   string
	HashedPassword string
	SignedUpDate   time.Time
}

func (p *profile) Name() string             { return "Michael Crilly" }
func (p *profile) SetName(name string) bool { p.RealName = name; return true }

func (p *profile) Email() string              { return "my@email.com" }
func (p *profile) SetEmail(email string) bool { p.EmailAddress = email; return true }

func (p *profile) Password() string                 { return "badhashedpassword" }
func (p *profile) SetPassword(password string) bool { p.HashedPassword = password; return true }

func (p *profile) SignedUp() time.Time             { return p.SignedUpDate }
func (p *profile) SetSignedUp(date time.Time) bool { p.SignedUpDate = date; return true }
```

Nothing magical here. Just returning some static information. Obviously a real implementation would use a database or some other data store. We're just going to work with static information.


