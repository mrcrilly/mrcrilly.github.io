---
title: "The LECT Engine"
date: 2018-04-16T07:00:00+01:00
draft: true
---

**tl;dr**

I'm working on a game engine called LECT (pronounced `lex`). It stands for Lore Mastery, Exploration, Combat, and Time. It's not the most original of names but in a nutshell these are the key aspects of the engine and they're what are going to make games built on the engine immersive, interesting, complex, challenging, and massive. In fact the goals that LECT solves for me, personally, are:

- Create games using only text and images, allowing for rapid and easy content creation by anyone
- Make it feel as though a player is walking through and exploring a book (text based adventure)
- Make worlds so big it takes months, maybe even years, to fully explore them (actual time)
- Allow for character builds that are complex and unique (traits)
- Combat is highly customisable and tailored to specific encounters (rotation tables)
- Force the player to think before acting (actual time)
- Make the player be patient and wait for actions to complete (actual time)
- The goal isn't shiny or the best equipment, it's defeating hard problems and being the best adventure the world as seen

These are the core tenants the engine will live by and aim to solve.

The lore (L) found throughout the world explains everything there is to be understood about the world. It's how you understand the what, where, why, and how of the world you're in. You need to study lore to open up the world map and begin exploring. Lore tells you the skill rotations used by certain creatures during combat (Beastology); how long it'll take to travel through a forest; or how-to craft a particular spell or potion. Lore leads you to exploration.

Exploration (E) is how you progress your character through the world. It's also how you find more lore to study. It's how you find foes to fight to get bigger and stronger, level up, stash away gold, get better gear, and move on through the world.

Exploring a dangerous world requires a good grasp of combat (C). Combat is, in essence, a modified, automated game of Magic The Gathering. It involves defining a rotation of skills and a set of reactions to certain events. During a combat phase your rotation is executed in order and your reactions trigger to events fired by your enemies, who also have skill rotation and reaction tables. Action Points (AP) are used to constrict what and when you can execute an ability.

Finally time (T) plays a key role in how you interact with the world. Moving from one town to another cannot be done instantly (to begin with) and takes (actual) time. Reading a book yields knowledge in the form of lore such as the part of the map becoming available or better understanding a monster's combat rotation. Restricting a player in this manner forces patience and allows the player to consider their actions carefully. It's like a (really complex) game of chess.

