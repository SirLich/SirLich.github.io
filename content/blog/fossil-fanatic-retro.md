---
title: "Fossil Fanatic Retrospective"
description : Retrospective for PULS Game Jam 2025
date: 2025-03-24
categories:
 - "programming"
tags:
 - "godot"
 - "gamedev"
---

![alt text](/images/fossil-fanatic-retro/end-screen.png)

Last weekend, I had the pleasure of re-joining the [Dash Splash](https://sirlich.itch.io/dash-splash) team along with some new faces in submitting an entry to the [PULS Game Jam 2025](https://itch.io/jam/puls-game-jam). You can [play our creation on itch.io](https://sirlich.itch.io/fossil-fanatic), and view the horrible [source code on github](https://github.com/SirLich/fossil-fanatic).

This will be my written retrospective of the experience, including some technical details.

## Friday

On Friday I was exhausted, and I knew I would be busy on Sunday, so I decided to stay home for the theme-reveal. I planned on being available as a backup programmer for my team, but I was otherwise not intending to join. This plan seemed to be working well, when at around 10pm I heard that they had found a Unity programmer to work with.

Even though I wasn't planning on jamming, I decided to sketch a few ideas for the theme: **Kaput** (*_broken and useless; no longer working or effective._)

![alt text](/images/fossil-fanatic-retro/idea-minigames.png)

The first idea that came to mind was some kind of space or submarine game, where the player had to play multiple minigames in real time, to keep their vehicle in operation. For example pumping oxygen, restarting the engines, or shooting aliens.

I figured this would be a good scope for a jam game, since you could simply keep adding minigames until you ran out of time. This hunch turned out to be prescient, since the overall winner [I hate this F@%$^ car](https://kubutek.itch.io/i-hate-this-f-car) used a similar idea to great effect (_and netting themselves €1000!_)

In the end my team couldn't find a suitable programmer, so I agreed to join them, albeit with limited time. The ideas they pitched were:
 - A fossil uncovering game
 - A stealth-inspired smash-stuff game

We ended up going with fossils, which I think was a great decision, due to the many smash-everything games I played during voting!

## Saturday

As this was my only full jam day, I knew it was important to nail down the game loop right away. We knew we wanted multiple tools, some kind of "digging" mechanic, and the possibility to damage the fossil(s). At first I hoped to do something with texture masking (think, erasing a layer slowly in photoshop), but I couldn't come up with a clever way of detecting when a fossil was uncovered, or how to apply damage, in case the player would dig without care.

In the end I decided to go the "easy" path, and make each obstacle discrete.

This uncovered an interesting challenge, that Godot didn't have a good out-of-box solution for: How to detect shape-on-shape collisions, that respects stacking?

The goal was to have tools that smashed rocks, but wouldn't damage obscured rocks or fossils. This of course requires knowing the order/relationship of the different rocks in the scene, and detecting collisions with them.

![alt text](/images/fossil-fanatic-retro/hover-rocks.png)

For a single point, this problem isn't *too* bad. You simple get all collisions, sort them (however you choose -tree order is a good starting point), and return the first result. This will give you whichever rock was on top. 

The problem becomes a lot stickier once you want to make the tool a circle radius, instead of a single point. Essentially the problem reduces to a 2D shapecast *in the z direction*, which is something that just doesn't exist in Godot. You cannot use the same sorting trick as before, because this doesn't account for how the rocks are overlapping.

![alt text](/images/fossil-fanatic-retro/hover-rocks-points.png)

In the end, my solution was to take the easy problem (checking collision order at a single point) and just repeating it in a grid across the shape. Visualized as red points above. This solution, while conceptually ugly, ended up working perfectly; plenty performant enough, and not really noticeable for the end user. It also generalized well to other tools.

With the primary game loop complete, I spent the rest of the day integrating assets, adding animations, and trying to leave things in a good state for Sunday.


## Sunday

In the best case, I would not have spent any time jamming on Sunday. I had prior plans, and in theory another programmer was going to be available to bring the game to the finish line. In practice, I left things in a pretty bad state on Saturday, and our second programmer was a complete novice to Godot.

I ended up spending probably 4 hours finishing some critical systems alongside [priorblue](https://priorblue.itch.io/), including brushing mechanics, improved animations, new levels, and bug squashing.

## Results

Fossil Fanatic placed 4th out of 168, in both the community and jury vote. That put us safely into the top 20 "short list" that would be further evaluated by the Jury, in order to award prize money, across five categories. During this time, a number of juries streamed their playthrough of the games, including [Steinwallen](https://www.youtube.com/channel/UCTmHYQZukLJUxQDLEmbjrWQ) and [DerHauge](https://m.twitch.tv/derhauge/home). 

This is always a great time, and very informative. It's a good reminder how important play-tests are -something I should incorporate more into my non-jam projects. 

Final results were like this:

![alt text](/images/fossil-fanatic-retro/results.png)

## Closing Thoughts and Post Jam

Since I can't leave things in a half-baked state, I always dedicate a few extra hours to a post-jam release -fixing bugs, integrating missing assets, and generally bringing the experience closer to a polished product, without sacrificing the charm of a jam game. This is the version you an [play on itch.io today](https://sirlich.itch.io/fossil-fanatic).

Jamming is always fun -especially if you have a good team to work with. Big thanks to BR, Die Gamerei, and everyone else who helped make this happen. I hope to continue jamming to de-stress from... making games for a living 🤪