---
title: "Introducing: The 'Super Wish Lists' Series"
date: 2018-02-09T12:10:00+00:00
draft: true
---

Blogging and vLogging has always been fun for me, but time and focus have never been in sync. Today that changes, and I'd like to introduce you to a new series, a new project, I'm firing up to get my creative juices flowing and more importantly, share my knowledge with you amazing people.

## Email Sucks...
After I met my fiancé (soon to be wife) and moved to Australia, it became apparant that her family loved Christmas and celebrated birthdays to the max. There's nothing wrong with this, in fact it's awesome(!), but it was the way in which they organised themselves which struck me as inefficient and error prone: email. They sent big wish lists out via email. Yuck!

Email is great in many regards - it did its part to change the way we communicate as a species - but for handing around wish lists for birthdays, Christmas, and other times of celebration, it just doesn't do it for me. It wasn't long before I would "Reply All" my response to the friend or family member being celebrated, and just like that, the surprise had gone. It also didn't take long for two people to turn up at the party with the same gift. D'oh!

After not only giving but also witnessing this brutal act, I decided it would be cool to create my own app, a wish list app, that took care of this problem. I did figure some apps might already exist, but I wanted to create something of my own because it opened up a few opportunies:

* I could share the code, make it open-source, and everyone could enjoy it (or not)
* I could write about the process, as I'm doing right now
* I could vLog about it and get the OpsFactory channel back up and running!
* It would allow me to educate my self on some new topics, mainly iOS/Android mobile development
* Mostly importantly to me: I could help educate others whilst learning my self - **that's win/win right there**

I got excited for the prospect and after a bit of planning, here we are with the first post in the series.

So what's the project called?

## Super Wish Lists
A dorky name, I know - I even have the domain name - but it's going to solve the wish list problem my friends and family has. It'll solve it for you too because, you know, it'll be open-source software. Anyway what's the idea? What's it going to do? Let's get straight to the key points:

1. You can create a wish list and fill it with items you'd like for your birthday, Christmas, wedding, etc.
1. Now you invite friends and family to your wish list so they can view what it is you're asking for
1. Friends and Family can mark items as "buying" or "bought", and you'll **never know or see this act!**
1. The invited can even add items, which again you cannot see, allowing others to see what other gifts they're buying you
1. And finally they can leave notes and comments for each other, which you cannot see neither

The overall idea is super simple: you can organise your wish lists and others can keep track of who is buying what without you ever knowing. Nice! It's not a magical idea that's going to change the world, but I reckon it's going to be a fun project to write and eventually use. 

So what does the project's development process look like? What tech are we going to use? Today I'll talk about the former, how the project's development process is going to work, but the latter will come in another post about the architecture and will talk more to the technical details.

## A Three Part Saga
This is where it gets technical now. If you're not keen on the technical details, then everything at this point down to the "The Process" will likely bore you. You're also welcome to stay, of course.

The application will be broken down into three components:

1. A RESTful API written in [Go](https://golang.org/)
1. A CLI utility written in Go
1. And an iOS mobile app

... and that's it. At least for now. That's version `v1.0.0`. Future versions will see an Android version coming into fruition, but for now I'm focused on a three stage plan.

You might asking why a CLI utility? Well, writing a CLI tool will give us a big set of advantages:

1. It'll be fast to write and easy to use
1. It can be written in Go
1. It can be automated easily
1. It can be used to populate a database quickly using a `Makefile` (automation)
1. We can test the API and general flow easily

And I'm sure there are other reasons too. For me, that's quite sufficient in terms of why it's a good idea.

As for an iOS only app. Why not Andriod as well? Aren't we going to develop a crossplatform mobile application? Nope. Having sorted out plenty of advice on the topic of mobile development, especially for a simple application like ours, I've been advised to go native. That is, write the applications in native tongue: Swift for iOS and Kotlin (not Java) for Android.

In light of this advice, I'll be going iOS only for `v1`. We will look at Android at a later date, but not too far off into the distance.

### Where's the Web UI?
There won't be one. This application is a perfect example for a mobile based application. It's the kind of app you don't login to via a web browser, but instead open on your phone, make a few changes or adjustments, maybe three times a year, and close again. It's a low use app' and it's perfect for the mobile platform.

This isn't to say a web UI can't or won't exist in the future. It'll be an open-source project, right? Anyone can write the web UI, or any client they like, however they like, whenever they like. Maybe you'd like to contribute such a UI? :-)

For now, I'm sticking a three phase project consistening of API, CLI and mobile. I think you're going to love the ride.

## The Process
So how is all this going to come together to form a cohesive project with planned development cycles and educational content? Good question! I've broken the construction of each component into tasks, and each high level task not only represents a step towards the component coming to life, but a blog post on this very website, and a vlog on the [OpsFactory YouTube channel](https://www.youtube.com/opsfactory).

Here's what the process will look like:

1. I will complete a high level task and push the code upstream
1. A blog post will be written for your consumption
1. Shortly after the post goes up, a vlog will be put together discussing the same information
1. Rinse, repeat

With this process, we should see a **two week development cycle/sprint** produce a single unit of work and posts to the blog and vlog. That's the aim and you never know, the number of blog posts may actually increase to several per fortnight as I work on the code base. After all, I'm trying to help you learn from this as much as possible.

## The Learning Experience
This is going to be great for everyone involved. I'm super excited to be sharing this project with anyone and everyone who is interested in the process of software development and deployment. So what does the learning experience look like?

I get to improve my writing and vlogging skills. I love writing and vlogging, but I love sharing knowledge too. It's one of the skills we can all learn to do, and it costs nothing but time and a little bit of effort. I'm grateful for the opportunity to be able to share these skills with you, so a big thank you for reading and following along.

We all get better at programming software, both server-side and mobile! Server side development has always been a passion of mine, but I've never touched mobile development beyond the, "Hello, world!" examples and tutorials. It's deffinitely time for that to change. This project is going to enlighten me to a new world of software development, and I hope you'll join me because it's going to be a run and wild ride.

We get to contribute back into the open-source market. This has been something I've been meaning to do for some time now and despite the fact there are literally tens of thousands of projects to contribute to, I've never been more excited for this project right here.

How does having an actual live, real app, that you helped write, on the iOS app store sound? That's sounds amazing to me. With OpsFactory hosting a real, production ready deployment of the API, the iOS (and eventually Android) app will be able to begin saving lives... OK maybe not saving lives, but certainly making them easier that's for sure.

Finally, and most importantly to me, you lovely people get to learn as well, from the code, the blog and the vlog. At least that's my dream. I do this daily, for a living, and being able to reach out and help others learn these skills, regardless of race, creed, religion, and geographical location, is just amazing to me. Do let me know if I can or have helped you in anyway.

So **subscribe to [the channel](https://www.youtube.com/opsfactory) and follow along**. That helps me out, but more importantly **it helps you** out too. This is about you as much as it is me, so come along for the ride and let's learn something together.

See you soon!
