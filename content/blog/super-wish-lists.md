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

... and that's it. At least for now. That's version `v1.0.0`.

- The construction of the application, all three components (four when I introduce Android into the fold) are not only in the open because they will be OSS...
- I've broken the construction of each component into tasks, and each high level task not only represents a step towards the component coming to life, but a blog post and a vlog...
- So I'll be publishing a blog post whenever I complete a task, but I'll write it as I go...
- After the blog post is written and published, a vLog will follow on the OpsFactory YouTube channel...
- These two additional steps to the development process will offer a great opportunity for others to learn from my work, mistakes, errors, bugs, security issues, and as new technologies are introduced...
- It'll be a great learning experience...
- Here is how you can help...
- Watch this space for the next article in the Super Wish List series: architecture! ...
