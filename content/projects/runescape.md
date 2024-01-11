+++
title = 'Runescape Server'
date = 2014-01-01
draft = false
+++

I spent a lot of time reverse engineering the game RuneScape to enjoy and learn. I originally saw other servers had done
the same thing but upon inspecting their code, I, somewhat naively, decided I was capable of doing better. I started 
from scratch and built a server from the ground up. I used other projects as a reference for the network protocol and 
data formats, as well as the obfuscated game client code. Usually, when someone announces they've written a private server 
for a game, they've just forked another project. That's not where I started - I started with a blank folder and a goal.

![](/projects/bots.png)

It took a few months to get to a point where a player could log in and walk around. I worked on and off,
and eventually implemented many of the core elements of the game: walking, npcs, dialogue, combat, skills, items, loot, 
attacks, magic and prayers, PvP, vendors, dynamically created maps and some special interactions. This was done
using a maven multi-module project with a core module and modules for various features. I had little real-world experience
so this made no use of dependency injection, hibernate or any other frameworks. I constructed my own event system and
plugin system, which was heavily influenced by the Bukkit server structure that I'd worked on previously.

This was particularly fun because of the challenges involved. Reverse engineering client code which was impressively 
obfuscated - far more than just variable names were changed. The network protocol which was impressively succinct. As 
the game was released in 2004, it was designed to work on dial-up internet connections, so the network protocol was 
designed to be as small as possible. Structures included significant bit packing, binary manipulation and compression.
The entire game from launcher to files was a ~130MB to download, and could be streamed in real-time delivering an almost
instant-launch experience.

Some community members contributed for a small period of time. The entire core project was ~55,000 lines of code,
not including scripts and plugins which were significant. I really enjoyed the challenge this project presented. It was
actually very helpful to maintain for a longer period of time, as I learned a lot about how to structure a project well.

### Tech Stack
* Java / MySQL
* Maven multi-module project
* Some BeanShell scripting, JavaScript scripting

### Challenges & Solutions
**Interactions** were a challenge. There seemed to be two approaches to this. The first was to have a callback for every
part of an interaction. This was not going to be suitable for me as I wanted to have a lot of interactions. The second
was what I chose, to have green threads. These were lightweight threads which could be paused and resumed. I used the
Quasar library to achieve this. This allowed me to write imperative code which was much easier to read and maintain.
This way, a sequence of actions could be written imperatively, with pauses in between, for example, animating an NPC,
waiting 2 seconds, then walking elsewhere and animating again. This was much easier to read and maintain than a callback
sequence of callbacks.

**Simple Server-Sided Bots** were a fun challenge. I wanted to have the world feel less empty, so I created some simple
bots which would be assigned goals and would work towards them. These included combat levels, acquiring items, gaining 
experience and fighting. These weren't using any machine learning, they were simple algorithms with some randomisation,
heuristics and memory of failures and successes. This was particularly enjoyable to see in action, since I could walk
around and watch the bots in game or watch them through the map viewer I built.

![](/projects/rune_bots.gif)
_Each dot represents a player which is being simulated and moving on the map to begin achieving its own generated goals. 
More on [YouTube](https://www.youtube.com/watch?v=FV6uD2vO_EM)._
