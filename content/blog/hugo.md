---
title: "Blogging with Hugo"
description : A quick introduction to the blog, and my experience with Hugo.
date: 2024-12-18
categories:
 - "programming"
tags:
 - "webdev"
---

Much like [passivestar](https://passivestar.xyz/posts/hugo/), I've chosen to start a blog using [Hugo](https://gohugo.io/). However unlike passivestar, I'm too ornery to use a pre-built theme. You're reading these words on my own homespun layout and theme, based on [100 bytes of CSS](https://dev.to/swyx/100-bytes-of-css-to-look-great-everywhere-19pd) that has been running around the internet lately.

In the last few years I've built a number of websites, with various techniques:
 - [VitePress, with default theme](https://wiki.sapiens.dev/guide/lua-getting-started.html)
 - [Self-written python SSG](https://sirlich.github.io/bedrock-schema-docs/)
 - [VitePress, with custom theme](https://wiki.bedrock.dev/)
 - [Hand written HTML](https://sirlich.github.io/)

I haven't particularly enjoyed building any of these sites. Hence Hugo. My review? It's fun!

The "happy" path of Hugo is clearly picking out a theme somebody else built, tweaking some configuration values, and tossing your markdown into the posts folder. But even the unhappy path isn't so bad. Hugo forces you to create a few files before it will render anything (e.g., `_single.html` and `_list.html`), but the setup is minimal. At the time of launch, I've written 181 lines of HTML templates, and 212 lines of CSS. All available in the sites github repository, of course.

The result is that I can create a site that looks exactly like I want, without bloat, and without writing a line of JavaScript or Go. I will call that a win!

I will be using this blog to write about technical topics within the realm of game development, game modding, and programming.