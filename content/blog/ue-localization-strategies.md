---
title: "UE5 Localization Strategies"
description : My yearly wishlist and resolutions for the technology I use.
date: 2025-09-01
draft: true
categories:
 - "programming"
tags:
 - "UnrealEngine"
---

By default, [Unreal Engines localization](https://dev.epicgames.com/documentation/en-us/unreal-engine/localization-overview-for-unreal-engine) is "author-at-source", which means that your primary language (say, English) will appear directly in your source code and Blueprints. When you localize, you're creating a mapping between an English string, and a secondary language. For example:
 - "Thank You" => "Dankeschön"

This is a very straight forward, comfortable workflow, and probably quite workable for individuals or small teams. However, it has some limitations, which can be solved with a different localization strategy.

The [localization documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/localization-overview-for-unreal-engine) from Unreal *does* mention a second technique they refer to as "author-once-and-reference", but they don't do a good job motivating why this strategy might be better. This article will cover this technique in more detail, including some tips and tricks I've picked up while implementing such localization in the past.

# Author Once Localization

In a nutshell, author-once localization works by defining a key format for your localization strings (e.g., `faction.ork.description`), and then creating key stores (either String Tables or CSV files) to hold them. Once this is setup, all strings (including those in your primary language!) should be considered "localizations" of the underlying term. No more scattering English strings throughout your codebase.

Note that by using unique keys for our terms, we're going one-step further than Unreals own definition of "author-once-and-reference". Just collecting terms into String Tables is *not enough* for what we want to achieve. 

## Reasons to switch

### Primary Language Support

For large operations, it's very common to use some sort of Localization service, whether that's a website where you can collaborate, or a fully external team you hire to do your translations. With Unreals default Localization you will discover that your primary language is treated "differently" than other languages, causing friction. 

For example changing "Dankeschön" to "Dankeschön!" can be achieved by changing a field on your localization website, and reimporting terms. But changing "Thank you" to "Thank you!" requires changing a value in source code, or perhaps opening Unreal and changing a Blueprint.

I've had one too many "Loc issue: x should be y" Jira tickets in my time. If a non-technical person wants to change a non-technical aspect of a game, they should be able to do it without getting an engineer involved!

### Stale Terms

If your uniquely identifiable key is "Hello World", and it changes to "Hello World!" you will find most localization services just shrug their shoulders, and clear all your existing translations. Sometimes this can be recovered from, but it's an endless game of wack-a-mole to repair translations that become broken after changing the primary language.

This is simply not an issue when using a term such as `generic.greeting`.

### Context Issues

Sometimes (though rarely), a term might be identical in English, but require different translations in other languages. This is a very contrived example, but the word "The" in English is always "The", while in German it could be "Der", "Die", "Das", etc..

By defining unique keys for every string in your game, you can ensure this is never an issue. Worried about duplicate translation efforts? Most services make this a non-issue by allowing you to combine terms under the hood.

# Implementation

Convinced? Then let's get started!

## String Tables vs. CSV

There are two reasonable ways to add key based localization to your project. You can pick whichever seems more convenient for you, but the rest of the article will assume you're using the Macros.

[String Tables](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-string-tables-for-text-in-unreal-engine) are a Blueprint asset that you create inside of the Engine (Misc -> String Table). This is a good option if you're not using C++ in your project.

Much more powerful is the `LOCTABLE_FROMFILE_GAME` macro which allows you to define a String Table in C++, which reads from a CSV file. Since most Localization services cab export this kind of CSV file, it's the most flexible way to work. As a bonus, it's possible to deal with merge conflicts in CSV files.

## 

## Defining Terms

The most critical 
