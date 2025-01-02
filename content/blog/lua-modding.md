---
title: "Modding in Lua"
date: 2023-12-28
description: I explain various techniques for modding games written in Lua.
draft: true
categories:
 - "programming"
tags:
 - "modding"
 - "lua"
---

This article will cover a few techniques for modding in [Lua](https://www.lua.org/). These techniques were used for modding [Sapiens](https://www.playsapiens.com/) but should be broadly applicable. Or at least provide an interesting window into the metaprogramming patterns available in the language.

# Level 0: Custom File Importing

The first level of modding is provided by the author of Sapiens directly, and allows us to "shadow" base game files, by placing our own `lua` file, in a location mirroring a base game file. For example, it's possible to modify `client/player.lua` by defining our own version at this location within the mod.

This is possible due to the `mjrequire` function, which seamlessly replaces the [require](https://www.lua.org/manual/5.1/manual.html#pdf-require) keyword.

# Level 1: Shadowing Utilities

As you can see above, the format for shadowing files 

