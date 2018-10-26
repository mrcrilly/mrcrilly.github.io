---
title: "Go REST API Base"
date: 2017-11-20T17:56:53+10:00
draft: true
---

I have a few projects I want to make a start on, but before I do I feel the
need to write out a base project, a template if you like, for quickly starting
a new micro service. I wanted something with a lot of best practices in place
from the get go. Something that would force logging, metrics, have a
healthcheck endpoint, and so on. Utilising the 12 Factor App methodology is
also important.

What I've ended up with so far, with a few days work, is a nice, clean project
with best-in-class libraries for getting a lot of the heavy lifting in place.

The projects I'm utilising to make this easier include:

- `Viper` for configuration management
- `httprouter` for fast, efficient handling of HTTP(S) requests
- `logrus` for handling logging and complex logging setups

The use of `Viper` and `httprouter` will come in a patch shortly when I
refactor to introduce them, removing my simple configuration handling (via a
struct and JSON marshalling) and Gorilla's mux for HTTP(S) handling.

The project can be found [over on
GitHub](https://github.com/mrcrilly/go-rest-template).
