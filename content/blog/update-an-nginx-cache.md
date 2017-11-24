---
title: "An (inflexible) way of updating nginx's cache"
date: 2017-11-24T19:07:50+10:00
---

I recently had a need to configure nginx to permit the updating of an item in
its cache. Trying to find any form of consistent opinion or material on this
matter is difficult. Many blog posts and Stack Overflow questions were read,
and most gave one of two opinions:

1. It can't be done, use a module to enable it;
1. It can be done using the `proxy_cache_bypass` parameter.

It turns out they're both right.

[I managed to prove](https://github.com/mrcrilly/nginx-cache-example) that
using the `proxy_cache_bypass` flag is indeed a valid way of updating an item
in the nginx cache. Simply put: when you send in a request with the correct
headers to your (`proxy_cache_bypass` enabled) nginx instance, the cache will
be bypassed, as you'd expect, but it will also be updated if the item on disk
is newer than the one in the cache.

This isn't obvious from the documentation at all. I'm not entirely sure I understand why the [nginx documentation
doesn't cover this
directly](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_bypass). It would be rather handy if they did and would likely save a lot of time and effort.

Consider giving the above Docker based setup a try. Just spin up the containers (after
building them) and throw a couple of cURL calls in a `watch` loop. Follow that
with updating the content in `backend/` and you'll see clearly the cache is
updated after you've bypassed the proxy.

Let me know if you've had other experiences or can provide a better solution.

(As a side note, nginx 1.12.1 was used for reasons.)
