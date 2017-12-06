---
title: "Vim"
date: 2017-12-06T18:40:24+10:00
draft: true
---

There are a lot of Vim tutorials out there. Vim has been around for quite some
time, so it's only natural for the Internet to be flooded with how-tos, guides,
introductions, and many other articles along the same lines. There are even
books. I don't want to introduce Vim or even write a tutorial, I simply want to
talk about it and how I use it.

I was actually opposed to using Vim for quite some time. Then I started using
it; I gave it a chance. I used it daily for roughly six months and then one day I
opened up a project in Microsoft's Visual Studio Code. I was pleasantly
surprised at how much functionality came out of the box, not to mention the
automatic plugin detection and easy installation. I moved over straight away
and Vim was left to gather dust.

I'm sure my little story has a predictable outcome: I started using Vim again
recently, and I'm not going back to another editor. I also recently changed
career, moving into a new role as a full time programmer. Previosuly I was a
Site Reliability Engineer (not at Google, unlike everyone on Hacker News, it
seems) so programming came in bits and bits, so my editor of choice wasn't a
big deal.

It turns out that crafting a Vim experience is addictive. Adding plugins and
shortcuts is a lot of fun and the possibilities are endless. At this point in
my Vim "career", I find my self spending 10-15 minutes per day adding some
plugin or refining the configuration of another. Over time, I think this will
deminish and I'll end up with a very well refined, powerful Vim installation.

I'm beginning to understand why people call this trade a "craft" - you
literally do build a chest of tools which you keep sharp, clean, and well
oiled. All that without even going into the actual topic of programming.

## Plugins

So without dribbling on for too long, let's look at the plugins I'm currently
using:

- [junegunn/fzf]()
- [junegunn/fzf.vim]()
- [fatih/vim-go]()
- [vim-airline/vim]()
- [scrooloose/nerdcommenter]()
- [Plug ]()
- [mileszs/ack.vim]()
- [ludovicchabant/vim-gutentags]()

I've listed the plugins above in their GitHub "path" style. If, like me, you're
using `Plug` for your plugin management, you can copy & paste the below into
your Vimrc if you wish to try out this configuration:

```
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug 'junegunn/fzf.vim'
Plug 'fatih/vim-go', { 'tag': '*' }
Plug 'vim-airline/vim-airline'
Plug 'scrooloose/nerdcommenter'
Plug 'elzr/vim-json'
Plug 'mileszs/ack.vim'
Plug 'ludovicchabant/vim-gutentags'
```

### Fuzzy Finding Files
[fzf]() and fzf.vim are used for fuzzy finding files from within your running
Vim instance. 

I don't claim to understand Vim's plugin system, but essentially what's
happening with the first line results in the `fzf` binary being installed on
your system. This is required as the fzf plugin for Vim simply utilises this
binary to do incredibly fast file system lookups, enabling you to do fuzzy
finding of files. It's very fast and it's very good. Give it a try. I replaced
[CtrlP]() with fzf.

Actually, the `fzf` binary can also be used outside of Vim,
including replacing the normal Bash history reverse-search (`ctrl+r`) for
searching your command history. It's actually rather nice.

### Go Development
With `vim-go`, you get almost everything out of the box for [Go]() development.
It'll even install all the binaries required to get going and can handle going
directly to definitions, building your code, installing a `main` package to
your `GOBIN`, running your tests, and so on. It doesn't leave much to be
desired.

Using `vim-airline`, I get a pretty status bar that gives me some useful
information, such as eord count, line number, character encoding, file type
(`markdown`, `php`, `python`, etc.) I also get a pretty list of my buffers
along the top of the window.

The `nerdcommenter` plugin allows me to easily comment or uncomment code with a
simple shortcut. It's not an overly complicated or fancy plugin, but Vim is
about crafting a tool that works with your mental model. It deserves a place in
my workflow as I use it often.

I don't think
