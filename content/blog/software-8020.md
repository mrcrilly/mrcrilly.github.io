---
draft: true
title: "Software: 80/20 It"
date: 2018-11-28T12:00:00+00:00
---

- I recently solved a simple problem within my family using a simple web app
- We needed a way of sharing wish lists for Christmas, birthdays and just about anything else we could find to celebrate
- I knew if I looked hard enough existing solutions would exist, such as Elfster, but I wanted more from the solution
- Firstly I wanted a learning experience from the solution, so writing it my self made sense
- Secondly I was surprised at how few options there actually were that did what we wanted: create a list of items people can comment on and mark items as bought without the "asker" of the gift knowing what is being said or who is buying what
- Thirdly, and this is mostly aimed at Elfster, I found the options immediately try to peddle you their wares or the wares of others using affiliate links (without telling you or being honest about it)
- A lot of the options also had horrible, slow UIs -- I hate excessive use, or exclusive use, of JavaScript to define and operate the UI
- So I wrote my own option, and when I did, I applied basic Agile principles (at least I applied my understanding of them) and the 80/20 principle
- Basic Agile principles dictate that a software engineer, or a team of engineers, should develop an MVP
- An MVP is, essentially, the bare minimum product that solves the problem being addressed in the most minimal, but usable, of ways
- So for [Super Wish Lists](https://superwishlists.com.au) (cheesy name I know) I needed a simple UI that allowed the users to:

* login
* create a list
* add an item to the list
* view other people's lists
* tag other people's desired items as "buying" or "bought"
* have it so everyone BUT the owner of the list/item can see the item has been bought by someone (preventing duplicate purchases)
* logout

- This setup is simple to get going. In fact it took a weekend of time, in total, using Go, Gin, SQLX, and a PostgreSQL database.
- To keep the development time down I did some things that, to my surprise, was incredibly enjoyable because it went against all contemporary views on web based software development:

* everything should be a REST API and React should be your UI layer... nonesense
* Instead I render everything server-side using Go's built in templating engine... yes I just said I render templates server-side
* I used the stock Bootstrap theme and only use the components they provide and minimal JavaScript
* I never implemented the ability for people to register an account nor even added support to email users
* I wrote a small CLI tool for managing user accounts, which took an hour, and I invited a few users to kick start the feedback loop for features and bugs by providing them with a password I defined
* I used simple `<ul>` list groups, a component Bootstrap provides, to list everything instead of trying to be a smart arse in the very beginning.
* I don't use JWTs and instead just use classic web cookies and a session token`- sue me
* I compiled everything to a single binary (it's Go, so this is somewhat obvious) and stuffed it, along with a small bit of custom CSS and the templates into a Docker image
* I deploy the Docker image to some DigitalOcean VMs ("Droplets") and setup a PostgreSQL DB

- All this took me a week of development time whilst holding down a full time job and having a (social) life
- It wasn't hard because I did something we should all do with software: 80/20 it

- The 80/20 principle has been covered and discussed to death by many, so look it up if you're unware of the concept
- In short I only did a small amount of the effort to solve the core 80% of the problem: let people have their wish lists and secret conversations
- The end result is a working system that the family is loving
- They love it because it solves a problem for them, but it's also lightning fast (stats?), simple, a clean interface (that can and will be improved on), no adverts or even pictures at this point, and is constantly being improved on

- Since implementing the system I have:

* Updated the UI to be more readable and add in additional information, removed information that was clutter, or added in key bits of hints and tips that make the experience better. for exmaple my father-in-law didn't want to provide a web link, store name and or a price estimate for each and every item, so those fields were marked as optional (which they always were to begin with) and this gave him the hint needed to get him using the system
* I added a "To Buy" list that listed the items you had marked and said you were going to buy for someone - like a shopping list of sorts
* Added the ability for people to "unmark" an item as being bought`incase they made a mistake in selecting an item
* Allowed people to leave a comment on an item or a list. Comments can be either hidden from the list/item owner (default) or marked as public so anyone can see the comment, encouraging conversation among family within the system

- These additional changes have taken a week an work fine. I'm sure there are bugs, but they will be ironed out in time as they're discovered
- This method of development feels sloppy and I have no doubt I have security holes somewhere or serious bugs, but the point is I'll find them in the end
- There's also no true Continuous Integration, Continuous Delivery, testing of any kind (I have strong opinions on testing I might write about) or anything to manager database schema migrations
- Deployments of a new version consist of me creating and pushing a new Docker image (`make docker-push`)
- Database migrations consist of me logging into the database server and applying a SQL file "patch" the schema (`psql -h $host -U $user $databasename < migrations/some-dated-sql-file.sql`)
- I then have Docker pull the new image, stop the existing container and run the new one (`make docker-run`)
- And just like that we have a working system that didn't need to be overcomplicated from the get go, or:

* use anything "modern" in terms of tech or methodology
* didn't need microservices coming out of the walls
* didn't need a Kubernetes cluster (although I am a big fan of Kubernetes; I'll be using Docker Swarm eventually)
* tests will come eventually in the form of behaviour testing, but weren't needed and helped launch the product in a weekend
