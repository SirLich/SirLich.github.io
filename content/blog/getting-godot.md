---
title: "\"Getting\" Godot: A Software Developers Perspective"
description : I explain the Godot engine architecture from a software developers perspective.
date: 2025-04-21
draft: true
categories:
 - "programming"
tags:
 - "godot"
 - "gamedev"
---

> Never had much luck with mainstream platforms like Unity that seem to want to "hide the code." 

I first came into contact with [Godot](https://godotengine.org/) in 2017. Despite my interest in both open source software and game development, it took me another 5 years of on and off experimentation to really "get" the engine Now I now use it as my daily driver for hobby projects and [game jams](https://sirlich.itch.io/).

The target audience for this article is experienced or skilled programmers who are trying to pick up Godot, and just don't "get" it yet. If you're already skilled in another engine (e.g., [Unity](https://unity.com/) or [Unreal Engine](https://www.unrealengine.com/en-US)), then this article may not apply to you.

*Caveat: Godot is a very flexible engine, and you can use it effectively in any number of ways. The insights in this article can necessarily only cover a small portion of these workflows. I will be focusing on what I consider the "standard" Godot experience.*

# Code First Workflows

By and large, Godot is not a "Code First" engine. This can be a little startling from a programmers perspective. Most software (websites, apps, tools, applications) start with some codebase, and only comes alive when you press compile or run. There is usually some [entry point](https://en.wikipedia.org/wiki/Entry_point) where you initialize your state, and if you chose, start an infinite loop to run some logic on repeat (e.g., collecting user input). If you've made minigames in a general purpose programming language, this should be familiar to you: *You write the code, you run the code, and there is your game.*

Godot simply doesn't function like that. This noticeable in three ways:
1. It has an editor
2. Some systems (such as user interface) are primarily built in-editor, not with code
3. The core "game loop" is already in place, and you can simply hook into it

## Why the Editor?

You must remember that games are not primarily created by programmers. They are a broad collaboration between programmers, musicians, artists of all kinds, and game designers. While the core game logic must be implemented in some programming language, many auxiliary systems such as particles, animations, and user interface design are more comfortably created using dedicated tools and editors.

While it is perfectly possible to use Godot without the Editor, many would consider this an anti-pattern. If you're very interested in code-first workflows, then engines such as [Bevy](https://bevyengine.org/) or [Raylib](https://www.raylib.com/) are worth exploring.

# Game Loop and Scene Tree

I mentioned above that the core game loop in Godot is abstracted away. When you start a new project, there is no `main.gd` file with a `main` function. There isn't an apparent place to print `"Hello World"`, or write initialization logic.

The reason for this is that Godot has handled all of this for you, with their implementation of the [Scene Tree](https://docs.godotengine.org/en/stable/classes/class_scenetree.html#class-scenetree). This is the class in the Engine that does all the setup, and starts the world ticking. In other words, when you want to start programming in Godot, you *don't* create or modify the programs entry point. Instead you add things to the scene tree, and let Godot tick and initialize them.

## Nodes

The things that we can add to the scene tree are called [Nodes](https://docs.godotengine.org/en/stable/getting_started/step_by_step/nodes_and_scenes.html). They are pre-defined [objects](https://en.wikipedia.org/wiki/Object-oriented_programming) that you compose together into [Scenes](https://docs.godotengine.org/en/stable/getting_started/step_by_step/nodes_and_scenes.html#scenes). This will form the backbone of your project. 

Without writing a single line of code, it's possible to create a facsimile of a game using nodes alone. For example you can place a `StaticBody` floor, and a few `RigidBody` balls, and they will bounce around and behave as expected.

Go ahead and try to do this now. Create a scene called `main.tscn`, and add some physics nodes as I've suggested above. 

## Scenes

Scenes in Godot are collections of Nodes that are save to a file. They can be instanced, nested, and played in the editor as a "level". They are a flexible paradigm that fully replaces the following concepts in many other game engines: Component, Actor, Prefab, and Level.

# Creating your first Scene

As I alluded to above, it's possible to create the basic outline of a game directly in the Editor by composing together nodes -no coding required. Go ahead 

# Sharp Corners

Before I dive any further, I want to address some "sharp corners" in GDScript that can be of particular annoyance to seasoned programmers. I will address some of these in more detail later on, but best to get them out of the way up-front:

- GDScript does not have imports
- GDScript does not have namespaces
- A `.gdscript` file is implicitly a class
	- Any additional classes will therefor be "nested"
- Constructors are a bit of a trap due to how objects are constructed

## Writing your First Script

"I just want to write some damn code!" you say.

## Types of Scripts

As you have seen, it is possible to attach scripts directly to Nodes, thus allowing us to script the functionality of our project. Callbacks such as `_ready` and `_process` as well as signals allow us to structure when and how our code would be executed. Building on this example, let us discuss the types of scripts you will most likely want to create:

### Static Functions and Helpers

Functions and variables in Godot can be annotated with the [static](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_basics.html#static-functions) keyword. 

# Common Misconceptions

## 

## No Imports

