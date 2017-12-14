---
title: "Vim"
date: 2017-12-06T18:40:24+10:00
draft: true
---

**tl;dr** I enjoy using Vim and crafting it into a lean tool for programming
with in multiple languages. I have my Vimrc file [over here on
GitHub](https://github.com/mrcrilly/vim) and if you decide to clone the repo to
`~/.vim`, a simple `vim +PlugInstall` should see you right (except for Ack and
Gutentags - they need some additional work.)

---

There are a lot of Vim tutorials out there. Vim has been around for quite some
time, so it's only natural for the Internet to be flooded with how-tos, guides,
introductions, and many other articles along the same lines. There are even
books. I don't want to introduce Vim or even write a tutorial, I simply want to
talk about it and how I use it.

I'm pretty much talking to my self here.

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

---

## The Leader Key
I've set my leader key to `,`. It can be anything you like, but given the way I
position my hands on the keyboard, I've chossen this key. With the key set, I
follow some simple guidelines for defining shortcuts.

When I add a new plugin, like the `vim-go` plugin which introduces a lot of Go
programming related interfaces to various Go binaries, I want to access some of
those commands quickly. What I tend to do is pick a letter to represent the
plugin. In this case I picked `g` for `vim-go`. Then I select a second letter
for the given shortcut. As a result, I have `,gb` set to run `:GoBuild` and
`,gt` set to run `:GoTest`.

This is how I use my leader key.

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

As a side note, the `install --all` command used for `fzf` installs the `fzf`
binary on your system. This works fine on macOS and Linux, but I don't know how
it behaves on Windows, if that's even a valid option.

### Fuzzy Finding Files
[fzf]() and `fzf.vim` are used for fuzzy finding files from within your running
Vim instance. It makes opening files into a new buffer super simple. It also
includes options for searhcing through open buffers, making it easier to switch
between a large range of open buffers.

I replaced [CtrlP]() with fzf.

Note: the `fzf` binary can also be used outside of Vim, including replacing the
normal Bash history reverse-search (`ctrl+r`) for searching your command
history. It's rather nice.

### Go Development
With `vim-go`, you get almost everything you need out of the box for [Go]()
development.  It'll even install all the binaries required for linting,
testing, and can handle going directly to definitions, building your code,
installing a `main` package to your `$GOBIN`, and so on. It doesn't leave much
to be desired.

### Status Bar
Using `vim-airline`, I get a pretty status bar that gives me some useful
information, such as word count, line number, character encoding, file type
(`markdown`, `php`, `python`, etc.) I also get a pretty list of my buffers
along the top of the window.

I've been taught that using buffers versus multiple windows is the correct way
to use Vim. I couldn't agree more. Although it's unlikely I would experience
performance issues if I used windows instead, it's still correct practice, and
`vim-airline` helps with this focus because of its buffers bar.

### Comments
The `nerdcommenter` plugin allows me to easily comment or uncomment code with a
simple shortcut. It's not overly complicated but Vim is about crafting a
tool that works with your mental model. It deserves a place in my workflow as I
use it often.

### JSON
I don't think the JSON plugin, `vim-json`, needs much introduction. It
essentially makes working with JSON nicer, increasing its readability. Check it
out.

### Ack
Now we've getting to the serious stuff. The `ack` plugin allows me to use [The
Silver Searcher]() for finding patterns inside of files. This means I can look
for a piece of code I might need to get a particular job done or perhaps find a
class I need to inherit from.

The plugin along requires some additional work to get going, but as this isn't
a tutorial I won't go into details.

### Gutentags
The `ctags` binary is used to parse the sources files for 44 different
programming languages. This enables one to highlight a type or function call
and jump to the definition. What `gutentags` does is manage the tags stored in
the tags file in a more intelligent manner versus simply running `ctags -R`
perodically. It can also manage where the file is stored, such as either in the
local source directory you're working in or somewhere else you can define
(you'll see what I do in this regard later when we look at my Vimrc.)

## Vimrc
This is my favourite part about Vim - the configuration. This is where you can
really craft a tool that works the same way as your work flows and thought
patterns. With other editors you can of course update their configurations and
manipulate the editor to do things your way, but I'm confident nothing comes
close to Vim (except maybe emacs, but I've never tried it.)

My Vimrc evolved quickly as I started using it for serious work. It continues
to evolve over time, but this is becoming less frequent. I'm down to about
10-15 minutes per day at the time of writing (as I said earlier.)

Let's go over the Vimrc in not a lot of detail because it will likely change,
making this configuration somewhat redundant within about a week.

### Plugins
Here is the plugins block:

```
call plug#begin('~/.vim/plugged')
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug 'junegunn/fzf.vim'
Plug 'fatih/vim-go', { 'tag': '*' }
Plug 'vim-airline/vim-airline'
Plug 'scrooloose/nerdcommenter'
Plug 'elzr/vim-json'
Plug 'mileszs/ack.vim'
Plug 'ludovicchabant/vim-gutentags'
call plug#end()
```

### Theme
Solarized is the only way to go in my opinion:

```
let g:solarized_termcolors=256
let g:solarized_termtrans=1
" wget https://raw.github.com/altercation/vim-colors-solarized/master/colors/solarized.vim
colorscheme solarized
```

### "Tabs"
It took some time, but eventually I got used to using buffers instead of
windows for handling mutliple files. However, instead of using `b` to
"represent" buffers, I decided on `t` for "tab":

```
nmap <leader>tn :enew<CR>
nmap <leader>tc :bp <BAR> bd#<CR>
nmap <leader>tr :bprev<CR>
nmap <leader>ty :bnext<CR>
```

### Fuzzy Finding
I've only got three options in place at this point in time:

```
nmap <leader>p :Files<CR>
nmap <leader>P :GFile<CR>
nmap <leader>B :Buffers<CR>
```

I also configure `ag` (`The Silver Searcher`) as such:

```
let g:ackprg = 'ag --nogroup --nocolor --column'
```

### Windows
I actually don't use windows much at all. I prefer to simply use buffers or
tabs in iTerm. I find them easier to work with. I do have options set, however:

```
nmap <leader>whs :split<CR>
nmap <leader>wvs :vsplit<CR>
nmap <leader>wc :q<CR>
nmap <leader>wq <C-W><C-J>
nmap <leader>we <C-W><C-K>
```

### Go Programming
Go is my favourite programming language. I've set a few options and
I've got access to a range of Go's tooling with a quick shortcut:

```
nmap <leader>gr :GoRun<CR>
nmap <leader>gb :GoBuild<CR>
nmap <leader>gi :GoInstall<CR>
nmap <leader>gt :GoTest<CR>
nmap <leader>gl :GoLint<CR>
nmap <leader>gf :GoFmt<CR>
```

Another key configuration item is to replace `vim-go`'s default `go fmt` and
replace it with `goimports`:

```
let g:go_fmt_command = "goimports"
```

### Invisible Characters
I usually keep these on. I've often found little issues in Python code and
generally think they're very helpful for most tasks:

```
set listchars=tab:▸\ ,eol:¬
nmap <leader>I :set list!<CR>
```

### Guten Tags
- I aim to ignore files I tend not to deal with

```
let g:gutentags_ctags_exclude = ['*.css', '*.html', '*.js', '*.c', '*.cpp', '*.java', '*.pl', '*.py', '*.rb']
let g:gutentags_cache_dir = '~/.vim/gutentags'
```

