---
title: "Little Puppet Boy Retrospective"
description : Retrospective for Global Game Jam 2026
date: 2026-02-05
categories:
 - "programming"
tags:
 - "godot"
 - "gamedev"
---
![alt text](/images/puppet-boy-retro/intro.png)

[Global Game Jam 2026](https://globalgamejam.org/) has come and gone. This is my retrospective for [The little Puppet Boy](https://globalgamejam.org/games/2026/little-puppet-boy-0), a top-down 2D fighting game with a story. The theme was "Mask".

-> [You can play on Itch.io here.](https://sirlich.itch.io/the-little-puppet-boy)

# Pitches and Team Building

From the start of the jam, it was pretty clear that my regular team was going to be jamming together. We had attempted to join the [ARD Game Jam – Classical Edition](https://games.ard.de/gaming/classical-game-jam), but were not accepted. I suppose if we had been accepted to the ARD Jam, then we wouldn't have worked together for GGJ. It's good to meet new people after all.

In any case, I pitched an idea, and [Phils Harmony](https://philsharmony.com/) and [Neon Flores](https://www.neonflores.com/) liked it well enough to join me!

**My pitch**: An "infinite" boss battle, where every time you defeat the boss, his mask falls of... revealing another mask beneath! Each mask would change the move-set of the boss.

Here is a sketch I did:

![alt text](/images/puppet-boy-retro/sketch.png)

After everything settled down, two more members had joined our team: [Jodeka](https://github.com/jiffjoff) (programming), and [Alec Shea](https://alecshea.bandcamp.com/) (VO, Writing, Music).

# Development

Something I did differently this jam was creating and using a [jam template](https://github.com/SirLich/godot-jam-template). This helped streamline the repository setup, but it didn't save me as much time as I hoped. Here are some issues I had (and improvements I want to make):
- Export templates were not configured to export the markdown file which contained the credits :/
- The SoundManager plugin I'm using isn't powerful enough in some cases, causing friction with [Philip](https://philsharmony.com/)
- Template was lacking many utils and helpers, which I had to pull out of other projects

I will improve the template for next time.

Beyond using the template, I would say the programming for this jam was pretty unextraordinary. There weren't any  tough programming challenges to solve, and as usual, I spent more time doing asset integration (animations, sfx, cutscenes) than I did writing gameplay code. It was a pleasure to work with [Jodeka](https://github.com/jiffjoff) for the first time. Although he wasn't very experienced with Godot, he caught on quickly. Some scenes (such as the credits sequence) were done entirely by him without my involvement. Awesome!

# Story and Voice Acting

From the first moments of development, it was clear that the game was going to be uniquely challenging to develop. For the first time we had a team member interested in writing and voice acting. Somebody indeed *specialized* in comedy VO and writing. Balancing the practical needs of combat and boss mechanics against the integration of a voiced storyline really was the defining challenge of the jam.

The game consists of four bosses which you fight in sequence. Each boss represents an emotion of your estranged father, as he grapples with his dissaproval of your choice to become a puppet master. Between each boss there is a cut-scene transition with dialogue, and during the fight, additional voice lines play in sequence, providing additional weight to the story.

The end result is pretty unique, and as my wife put it "very very different from your other games" :')

![alt text](/images/puppet-boy-retro/puppet-joy.png)
![alt text](/images/puppet-boy-retro/puppet-sadness.png)

# Success?

How do you judge the success of a jam project?

Completing a game in any capacity is it's own reward. Meeting new people and forming connections is a reward. Polishing a game and honing your craft is a reward. But perhaps the best reward of ALL is coming out of the jam with a new game idea, *and that's something that you only get when you take risks*.

If you play many jam games, you will find a *lot* of terrible ideas. Games that combine genres that shouldn't be combined. Games that remove the players ability to play properly. Game ideas so silly and weird that you couldn't sell them on steam even if you had a large development team and 3 years to bring the idea to market.

And these games are wonderful. Jams are safe spot to try out daring ideas, and sometimes those ideas turn out great! Innovative games like [Baba Is You](https://hempuli.itch.io/baba-is-you) got its start as a jam game.

At first, I was very nervous about trying to integrate a voiced story. It felt like it would fight for attention with the bossfight mechanics. I wanted to take the safe route, as I've done in years past: Simple idea, oodles of polish, and call it a day. But I've done that before, and honestly, there is only so much you can learn from that.

It was nice to work on a more interesting concept this year.

Till next time! 

![alt text](/images/puppet-boy-retro/apathy.png)
![alt text](/images/puppet-boy-retro/anger.png)
