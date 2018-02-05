---
title: "Go Testing: Moq and gotests"
date: 2018-02-04T00:40:17+01:00
draft: true
---

I recently getting more involved with writing tests at work. One thing I noticed with our code was a lot of function pointers in structs. When I queried what this was for I was told, "For mocking out the functions for easier testing." That's certainly one way to do it, but there's deffinitely a better way.

## tl;dr
Using Moq and gotests, I've been able to rapidly develop mock frameworks for my interfaces and also generate table driven tests for my implementations. Now I can easily test complete implementations of my interfaces but also mock out any dependencies needed with little to no work at all.

On the CLI I would:

1. `moq -out interface_mock.go . interface`
1. `gotests -all -w type_test.go . type.go`

Replacing `interface` and `type` accordingly.

## Interfaces
Interfaces are one of Go's most underutilised features. They can be somewhat confusing and hard to get your head around, but when they're put in place they allow the above situation to be handled in a much more elegant manner. 

For those who are new to Go, let's define a quick interface so we have an example to work with throughout this article.

```

//go:generate moq -out user_mock.go . Profile
//go:generate gotests -all -w profile.go

// Profile abstracts how a profile behavours.
// Primarily added for mock-ability.
type Profile interface {
	RealName() string
	SetRealName(name string) error

	Age() uint
	SetAge(age uint) error

	DOB() *time.Time
	SetDOB(dob time.Time) error

	Location() (string, string)
	SetLocation(city, country string) error

	LinkedLogins() []login.Login
	AddLinkedLogin(login login.Login) error
	RemoveLinkedLogin(id string) error
	DisableLinkedLogin(id string) error

	Friendships() []friend.Friend
	AddFriendship(friend friend.Friend) error
	RemoveFriendship(friend friend.Friend) error
}
```

We'll get into the `//go:generate` lines later.

This is a "simple" interface for a user profile type. This is a contract for other packages in my application to utilise and have guarantees about behaviour. I like this structure of placing concrete types in their own packages. maybe that's something to be explored in another post.

## An Implementation
Let's write a simple implementation for the interface above.

```
// UserProfile represents a human readable profile for a user.
// This profile is static, but can have multiple logins bound to it.
type UserProfile struct {
	Realname    string
	UserAge     uint
	DateOfBirth time.Time
	City        string
	Country     string
	Logins      []login.Login
	Friends     []friend.Friend
}

// RealName well return the Realname field for a user.
func (p *UserProfile) RealName() string { return "" }

// SetRealName well update the Realname field for a user.
func (p *UserProfile) SetRealName(name string) error { return nil }

// Age well return the UserAge field for a user.
func (p *UserProfile) Age() uint { return 0 }

// SetAge well update the UserAge field for a user.
func (p *UserProfile) SetAge(age uint) error { return nil }

// DOB well return the DOB field for a user.
func (p *UserProfile) DOB() *time.Time { return &time.Time{} }

// SetDOB well update the DOB field for a user.
func (p *UserProfile) SetDOB(dob time.Time) error { return nil }

// Location well return the City, Country fields for a user.
func (p *UserProfile) Location() (string, string) { return "", "" }

// SetLocation well update the City, Country fields for a user.
func (p *UserProfile) SetLocation(city, country string) error { return nil }

// LinkedLogins well return the Logins field for a user.
func (p *UserProfile) LinkedLogins() []login.Login { return []login.Login{} }

// AddLinkedLogin well add a Login to the Logins field for a user.
func (p *UserProfile) AddLinkedLogin(login login.Login) error { return nil }

// RemoveLinkedLogin well remove a Login from the Logins field for a user.
func (p *UserProfile) RemoveLinkedLogin(id string) error { return nil }

// DisableLinkedLogin well disable a Login in the Logins field for a user.
func (p *UserProfile) DisableLinkedLogin(id string) error { return nil }

// Friendships well return the Friends field for a user.
func (p *UserProfile) Friendships() []friend.Friend { return []friend.Friend{} }

// AddFriendship well add a Friend to the Friends field for a user.
func (p *UserProfile) AddFriendship(friend friend.Friend) error { return nil }

// RemoveFriendship well remove a Friend from the Friends field for a user.
func (p *UserProfile) RemoveFriendship(friend friend.Friend) error { return nil }
```

Nothing magical here. Just returning some static information. Obviously a real implementation would use a database or some other data store. We're just going to work with static information so we can explore the concepts surrounding mocking and table driven tests.

## Moq
So we have an interface and an implementation of it (which obviously comes with function/sreceivers that need testing.) Let's now take a look at Moq.

If we invoke Moq directly, like so: `moq -out user_mock.go . Profile` we will get a big file called `user_mock.go` containing, as you might have asked, a mocking "framework" for our `Profile` interface. I call it a framework because it comes not only with an object we can use for mocking the interface and testing its methods, but also a simple means of tracking the call stack along with the parameters passed to each receiver.

### ProfileMock
The actual mocked interface looks like this:

```
type ProfileMock struct {
	// AddFriendshipFunc mocks the AddFriendship method.
	AddFriendshipFunc func(friend friend.Friend) error

	// AddLinkedLoginFunc mocks the AddLinkedLogin method.
	AddLinkedLoginFunc func(login login.Login) error

	// AgeFunc mocks the Age method.
	AgeFunc func() uint

	// DOBFunc mocks the DOB method.
	DOBFunc func() *time.Time
	
	// ...
	
	// calls tracks calls to the methods.
	calls struct {
		// AddFriendship holds details about calls to the AddFriendship method.
		AddFriendship []struct {
			// Friend is the friend argument value.
			Friend friend.Friend
		}
		// AddLinkedLogin holds details about calls to the AddLinkedLogin method.
		AddLinkedLogin []struct {
			// Login is the login argument value.
			Login login.Login
		}
		// Age holds details about calls to the Age method.
		Age []struct {
		
		// ...
	}
}
```

I've contracted this down to a few fields for readability. The actual struct is massive.


