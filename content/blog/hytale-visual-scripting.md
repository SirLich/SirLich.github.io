---
title: "Visual Scripting & Hytale"
description : Personal musings on the efficacy of Visual Scripting
date: 2025-10-19
categories:
 - "programming"
tags:
 - "modding"
 - "blueprint"
---

Hypixel Studios recently published a [blogpost](https://hytale.com/news/2025/11/hytale-modding-strategy-and-status) about the state of modding in [Hytale](https://hytale.com/), including plans to offer a [Visual Scripting](https://en.wikipedia.org/wiki/Visual_programming_language) language instead of a text-based scripting solution (e.g., [Lua](https://en.wikipedia.org/wiki/Lua), [JavaScript](https://en.wikipedia.org/wiki/JavaScript)).

Here is the excerpt, in it's entirety:

> #### Why we're not offering text based scripting:
> A common question: "Where's Lua/scripting?"
> Short answer: We do not have text-based scripting and we do not intend to add it.
> Here's why:
> - Text-based scripting is usually introduced to "help non-programmers" like designers building custom behaviours.
> - In reality, script languages like Lua are still programming languages:
> - Programmers now have to juggle two languages, one of which usually feels "nerfed".
> - Designers are still expected to learn actual programming concepts.
> - In the end, it's less inclusive and increases complexity for both sides.
> We see that as a false compromise.
> Our Direction: Visual Scripting
> #### Instead of text-based scripting, we will add visual scripting:
> Our experience with Unreal Engine Blueprints showed us that:
> - Designers feel genuinely empowered when they can build logic visually.
> - Programmers are more productive when they stay in a programming language (Java/C#) and expose high-level nodes.
> #### The goal:
> - Designers are empowered through a visual language that matches how they think about behaviours.
> - Programmers can extend and optimize this system by adding new visual nodes and performance-sensitive implementations.
> - We avoid fragmenting logic across multiple "half-languages".
> 
> We believe this is the most empowering approach for modders without compromising on capabilities.

## False Dilemma

I'm perfectly at peace with Visual Scripting (VS) existing alongside more robust programming languages. Especially if it's possible to write chunks of code in those programming languages, and expose them to VS via nodes. I spent multiple years doing just that in Unreal Engine.

My issue is that I think the choice between VS and text-based scripting is simply a false dilemma. A good, modern visual scripting implementation should reduce to text anyways. Because if it doesn't...

## The Horrors of Binary

If you've ever worked with Blueprint, you might have encountered some of these frustrations, all caused by the fact that Blueprints are binary:

- Version control is difficult
  - No easy code review
  - No easy code diffing
  - No easy merge conflicts
- Snippets cannot easily be shared
  - Help-requests come as blurry screenshots
  - Micro libraries or examples are hard to share
- No easy transpiling
- Assets can become corrupted
- LLMs cannot interact with them*


*Included for completeness. I don't personally find this to be important.
