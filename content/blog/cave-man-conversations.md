---
title: "Cave Man Conversations Retrospective"
description : Retrospective for Ludum Dare 59
date: 2026-04-20
categories:
 - "programming"
tags:
 - "godot"
 - "gamedev"
---

[Ludum Dare is ending](/blog/ludum-dare/). But it's not over yet, so it's time to jam! Unlike all of my previous Ludum Dare submissions, I chose submit to the "Jam" category, which meant finding a friend to work with!

My partner in crime is [Mischa](https://mischa2341.itch.io/), a fellow programmer and Godot novice. Two programmers, no artist... uhoh! I was worried we wouldn't have the required skills to make a good game, but in the end it didn't end up mattering. I took over 2D art, Mischa did music, and we collaborated on everything else.

Two people makes for a good team size, I think.

## Theme Announcement and Ideas

The theme was announced 3am our time, so neither of us saw the theme until the next morning: SIGNAL. I will admit, this theme did *not* spark joy. I always start with a kind of brain map, and nothing was sticking:
- Signal fire
- Signalling gun
- [Signal](https://signal.org/) (IM)
- [SETI](https://www.seti.org/)
- Naval signalling flags
- [Semephore towers](https://en.wikipedia.org/wiki/Semaphore)

The biggest issue we faced, is that most of our ideas would play best as a multiplayer, or local multiplayer experience. Think, a minigame for [JackBox](https://www.jackboxgames.com/games/packs). While temping, this just isn't wise for a game jam! You usually get too little feedback for it to be worth it. 

In the end, we decided to take a "multiplayer" game, and do one half of it. As you will see, this turned out to be a perfect decision!

## The Initial Idea

The initial idea, was to build one half of a pictionary style communication game. You would see a message sent over smoke signals, which you would interpret back into the original message. For example this symbol should be interpreted as "Hello":

![alt text](/images/cave-man-conversations/hello.png)


## The Wild Wild West

For some insane reason, we got stuck in the idea of sitting at a camp fire in the wild west. Mischa recorded camp songs on his guitar, and I draw a beatiful Utah sunset. 

![alt text](/images/cave-man-conversations/wild_west.png)

Then we sat together and stared at our handiwork. And it didn't look good 😱

We were aware that actual [smoke signals](https://en.wikipedia.org/wiki/Smoke_signal) were a far cry from the pictograms we were going to be using. And because we wanted to use one pictogram per word, the actual language of the message was going to be quite "cave man" coded. We felt it was prudent to pivot the theming of our game, to avoid drawing any unwanted comparisons to the [native peoples of the region](https://en.wikipedia.org/wiki/Native_Americans_in_Utah).

## Grog to the Rescue

The pivot was pretty easy: Just lean harder into the cave-man theme! We rewrote some of the dialogue, gave the game a new name, and finally, reworked the art. I tried a few background paints that were more classically cave-man, but I didn't like them. In the end, I added a new foreground element on top of my original picture, and called it a day:

![alt text](/images/cave-man-conversations/game.png)

## Finishing the Gameplay

As we worked, we started to get the feeling that maybe the 2nd half of the game would be possible as well (sending messages). At first this seemed impossible, because what should the player communicate? How to verify that they communicated correctly? 

We realized that it was possible, as long as we prompted the player correctly (so they said what we wanted).

Coming up with the idea was actually harder than the implementation. We quickly threw together a panel for responding to the messages, and suddenly the game felt complete!

**First you would interpret a message:**

![alt text](/images/cave-man-conversations/guess.png)

**Then respond:**

![alt text](/images/cave-man-conversations/send.png)

## Technical Woes

We used my [Jam Template](https://github.com/SirLich/godot-jam-template), and it was less than smooth sailing. I gathered up a bunch of fixes and changes I will need to make for the next jam. It's hard to find motivation to work on the jam template outside of jam season, but you really pay for it during the jam!

I want to make some small non-jam games with the template, to refine it further. 

Till next time!