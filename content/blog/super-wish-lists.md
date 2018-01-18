---
title: "Super Wish Lists"
date: 2018-01-09T00:40:17+01:00
draft: true
---

I want to talk about a project I'm going to be developing on YouTube over the
next few months. My channel has been left to gather dust for nearly a year now
so it's time to get back into the game of making videos. I really love the
process and I think I have a good idea, so let's dive in.

## What's the project about?
I've always wanted to develop an application that resolves a small problem we
have in our family: Christmas and birthday wish lists. Poeple asking for stuff
by providing a list of possible gifts via email is a messy way of operating, so
I want to develop a mobile first means of managing this. 

It's not a super exciting project, but it's an excellent project for multiple
reasons:

- It gets my Go knowledge sharper as I develop the app
- It'll get my frontend knowledge up to scratch
- I can finally solve this minor(?) organisational issue within the
  family/social circle
- It'll be open source so it's perfect for a YouTube series covering varies
  aspects surrounding how the software is develop

## General architecture & design
...

## Monolith versus Microservices
- I've selected a modular monolith
- Microservices can come later
- RESTful API first, templates second
- Microservices come later when scaling is an issue
- Microservices aren't suitable for this project

## From stratch versus "framework"
- Don't learn much developing using a framework
- Frameworks are for getting work done fast: I'm not in a rush
- I'm a minimalist at heart, so I like to build from stratch so I can minimise
  dependencies and bloat

## Libraries to use
- sqlx
- httprouter

## Git work flow and repository
- Repository is located on GitHub here

## Project structure
- A lot of modules, allowing for splitting the app' into microservices in the
  future
- Interfaces will be used where they can, and should, be to enable dependency abstraction


## Logging and config
- Logrus gives us a lot of options and is nice and flexible
- Viper is an amazing lib for handling configuration for you

## Creating the model interfaces
...

## Creating structs for the model interfaces
...

## Web server interface? Probably not
...

## Dockerfile for database "infrastructure"
...

## CLI tool for manipulating the database
...

## CLI tool for CRUD ops against models
...

## Web server endpoints for CRUD ops against models
...

## Templates based on bootstrap
...

## Input validation: client & server
...

## Authentication
...


