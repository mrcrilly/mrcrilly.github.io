---
title: "Introducing: The 'Super Wish Lists' Series"
date: 2018-02-08T00:40:17+01:00
draft: true
---

Blogging and vLogging has always been fun for me, but time and focus have never been in sync. Today that changes, and I'd like to introduce you to a new series, a new project, I'm firing up to get my creative juices flowing and more importantly, share my knowledge with you amazing people.

## Email Sucks...
After I met my fiancé (soon to be wife) and moved to Australia, it became apparant that her family loved Christmas and celebrated birthdays fully. There's nothing wrong with this, of course, but it was the way in which they organised themselves which struck me as inefficient and error prone: email.

Email is great in many regards - it did its part to change the way we communicate as a species - but for handing around wish lists for birthdays, Christmas, and other times of celebration, it just doesn't do it for me. It was long before I would "Reply All" my response to the friend or family member being celebrated, and just like that, the surprise had one. Damn!

After not only giving or but also witnesses this brutal act, I decided it would be cool to createmy own app, a wish list app, that took of this problem. I did figure some apps might already exist, but I wanted to create something my self because it offered me a few opportunies:

* I could write about the process, as I'm doing right now
* I could share the code, make it open-source, and everyone could enjoy it (or not)
* I could vLog about it and get the OpsFactory channel back up and running!
* It would allow me to educate my self on some new topics, mainly iOS/Android mobile development
* I could help educate others whilst learning my self...

The list goes on. I got excited for the prospect and after a bit of planning, here we are with the first post in the series.

## Super Wish Lists
A dorky name, I know - I even have the domain name - but it's going to solve the wish list problem my friends and family has. It'll solve it for you too because, you know, it'll be open-source software.

So what's the idea? What's it going to do? Let's get straight to the key points:

1. You can create a wish list and fill it with items you'd like for your birthday (let's say...)
1. Now you invite friends and family to your wish list so they can view what it is you're asking for
1. Here's the interesting part: they can mark items as "buying" or "bought", and you'll **never know!**
1. The invited can even add items, which again you cannot see, allow others to see what other gifts you're gonna get
1. And finally they can leave notes and comments for each other

Nice! It's not a magical idea that's going to change the world, but I reckon it's going to be a fun project to get into place and just as fun to use.

So how is the application going to be built? What tech are we going to use? Today I'll talk about the former, how the application is going to be built, but the latter will come in another post about the architecture.

## A Three Part Saga
This is where it gets technical now. If you're not keen on thetechnical details, then everything at this point downwards will likely not interest you, but you're welcome to stay and read anyway.

The application will be broken down into three components:

1. A RESTful API written in Go
1. A CLI utility written in Go
1. And an iOS mobile app

... and that's it. At least for now. That's version `v1.0.0`. Future versions will see an Android version coming into fruition, but for now I'm focused on a three stage plan.

Why a CLI utility? Writing a CLI tool will give us a big set of advantages:

1. It'll be fast to write
1. It can be written in Go
1. It can be automated easily
1. It can be used to populate a database quickly using a `Makefile` (automation)

And I'm sure there are other reasons too. For me, that's quite sufficient in terms of why it's a good idea.

As for an iOS only app. Why not Andriod as well? Aren't we going to develop a crossplatform mobile application? Nope. Having sorted out plenty of advice on the topic of mobile development, especially for a simple application like ours, I've been heavily advised to go native. That is, write the applications in native tongue: Swift for iOS and Kotlin (not Java) for Android.

In light of this advice, I'll be going iOS only for `v1`. We will look at Android for `v1.1`, perhaps.

## Where's the Web UI?
There won't be one. This application is a perfect example for a mobile based application. It's the kind of app you don't login to via a web browser, but instead open on your phone, make a few changs or adjustments, maybe three times a year, and close again. It's a low use app' and it's perfect for the mobile platform.

This isn't to say a web UI can't or won't exist in the future. It'll be an open-source project, right? Anyone can write the web UI, or any client they like, however they like, whenever they like.

For now, I'm sticking a three pashe project consistening of API and mobile. I think you're going to love the ride.

## The Process
So how is all this going to come together to form a cohesive project with planned development cycles and educational content? Good question! I've broken the construction of each component into tasks, and each high level task not only represents a step towards the component coming to life, but a blog post on this very website, and a vlog on the OpsFactory channel.

Here's what the process will look like:

1. I will complete a high level task and push the code upstream
1. A blog post will be written for your consumption
1. Shortly after the post goes up, a vlog will be put together discussing the same information
1. Rinse, repeat

With this process, we should see a **two week development cycle/sprint** produce a single unit of work and posts to the blog and vlog. That's the aim. It may change if it becomes too difficult or give life takes over - only time will tell.

## The Learning Experience
This is going to be great for everyone involved. I'm super excited to be sharing this project with anyone and everyone who is interested in the process of software development and deployment. So what does the learning experience look like?

I get to improve my writing and vlogging skills. I love writing and vlogging, but I love sharing knowledge too. It's one of the skills we can all learn to do, and it costs nothing but time and a little bit of effort. I'm grateful for the opportunity to be able to share these skills with you, so a big thank you for reading and following along.

We all get better at programming software, both server-side and mobile! Server side development has always been a passion of mine, but I've never touched mobile development beyond the, "Hello, world!" examples and tutorials. It's deffinitely time for that to change. This project is going to enlighten me a new world of software development, and I hope you'll join me.

We get to contribute back into the open-source market. This has been something I've been meaning to do for some time now and despite the fact there are literally tens of thousands of projects to contribute to, I've never been more excited for this project right here.

Finally, and most importantly to me, you lovely people get to learn as well, from the code, the blog and the vlog. At least that's my dream. I do this daily, for a living, and being able to reach out and help others learn these skills, regardless of race, creed, religion, and geographical location, is just amazing to me.

## How can you Help?
The best way to help is to subscribe to the channel and follow along. That helps me out, but more importantly it helps **YOU** out. This is about you as much as it is me, so come along for the ride and let's learn something together.

See you soon!
