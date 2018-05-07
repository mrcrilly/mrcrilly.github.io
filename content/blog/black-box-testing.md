---
title: "Black box testing"
date: 2018-05-07T17:30:00+00:00
---

I recently needed to introduce testing to an authentication microservice I've been writing. Two things prompted this:

1. Testing is a good idea and offers certain assurances going forward
1. I was sick of manually testing the service myself using Insomnia and saved requests

The second reason shouldn't have come into fruition at all. Manually testing software is error prone and isn't done during a commit push to the remote repository. And reason one came too late. Tests should come first in the development process.

I opted for a Behaviour Driven Development (BDD) approach. Behaviour based tests are black box tests. They test your product from the outside by pushing its buttons and seeing what it does. If it doesn't do what you think it should do the tests fail. Changes to APIs, behaviour, units, modules, algorithms, and anything inside the box, are caught (if you've got the use cases covered.)

I considered the benefits of unit and module tests against simply testing the whole system in one go. Ultimately I don't care if a single unit is working as intended in isolation: I want the whole machine to work and conform to my requirements. If it's not confirming, I fix it. If I break something during a development cycle, I'll know before I even commit anything.

For more information on TDD, checkout this excellent conversation between [Martin Fowler, Kent Beck, and David Heinemeier Hansson](https://martinfowler.com/articles/is-tdd-dead/). Also read David's thoughts in his blog post, ["TDD is dead. Long live testing"].(http://david.heinemeierhansson.com/2014/tdd-is-dead-long-live-testing.html) Another good read is, ["Why most Unit Testing is a waste"].(https://rbcs-us.com/documents/Why-Most-Unit-Testing-is-Waste.pdf)

At first I started using [Ginkgo](https://github.com/onsi/ginkgo). It's a very mature, well established library for BDD. However it quickly got complex and confusing, and so I abandoned it in favour of [GoConvey](https://github.com/smartystreets/goconvey/).

To test a call to my service, I'm writing simple tests:

```go
func TestAuthenticationServiceJourney(t *testing.T) {
  Convey("The user can complete a journey through the service", t, func() {
    response := createNewUser(...)
    So(response.HTTPStatusCode, ShouldEqual, http.StatusOK)
    So(response.Error, ShouldBeFalse)
    
    response = loginNewUser(...)
    So(response.HTTPStatusCode, ShouldEqual, http.StatusOK)
    So(response.Error, ShouldBeFalse)
    // ...
  })
}
```

I originally wrapped the repeated `response` and `So()` lines into individual `Convey()` calls, but these generate their own scope and Convey acts a bit weird here. The wiki has the [execution method](https://github.com/smartystreets/goconvey/wiki/Execution-order) covered quite nicely.

I have a primary test for the whole journey (create new account, login, refresh JWT, update password, forgot password, logout, etc.) and individual tests for bad inputs, actions, or security.

I'm testing for three kinds of input:

1. Harmful input
1. Clumsy (invalid) input
1. Good input

On top of Convey, I've also started using [Fake](https://github.com/icrowley/fake) to generate email address, passwords, real names, and so on. Fake allows me to generate large testing tables of data and pass is through the various tests. This means I can get a wide variaty of inputs to ensure I'm not simply testing what I think should be tested, but instead testing what could, and likely will, be given to the API.

I'm going to continue moving forward with this testing mentality and see how it goes.
