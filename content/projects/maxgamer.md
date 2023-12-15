+++
title = 'MaxGamer'
date = 2010-01-01
draft = true
+++

![](/projects/MaxGamer.png)

This was a community I operated and moderated between 2010-2014. It was a
Minecraft server that started with some local players from my friend circle
that were looking for a community to play with. After opening it up to the
public, the community reached 75,000 unique registrations after its 5 year
life span. It was a fantastic hobby project during my time studying at
university where the majority of my time went into development and player
relations including events and community management.

The website was written in PHP 5 and made heavy use of MySQL and integration
with phpBB for account access. The custom authentication allowed a player to
register in-game or via the forum and access the same account. This site also
integrated with "top 100" websites, where players would vote for their favourite
community and that would bump the server up in the tier list, exposing the
server to more potential players. This included rewarding players in-game with
a small thank-you for boosting the server and helping grow the community. An
oddly challenging feat to integrate!

The server was operated on an Ubuntu machine remotely hosted in a cheap data
centre that was paid for through player donations. I administrated this almost
entirely through SSH and this was an incredibly valuable experience for me to
learn to operate a Linux server.

During my administration, I wrote a dozen or more server-side plugins in Java.
These included tools for:

* Looking up item names using a [trie](https://en.wikipedia.org/wiki/Trie)
* Raytracing a players view to prevent interaction through walls
* Custom PvP modes including last-man-standing survival challenges
* Administering account penalties on the server - kicks, mutes, bans
* Player to player item sales and transfers through in-game currency

A number of these were even published on [Bukkit](/projects/bukkit/)!
