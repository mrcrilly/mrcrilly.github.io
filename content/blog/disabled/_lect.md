---
title: "The LECT Engine"
date: 2018-04-16T07:00:00+01:00
draft: true
---

I'm working on a game engine called LECT (pronounced `lex`). It stands for Lore
Mastery, Exploration, Combat, and Time. It's not the most original of names but
in a nutshell these are the key aspects of the engine and they're what are
going to make games built on the engine immersive, interesting, complex,
challenging, and massive.

The goals that LECT solves for me, personally, are:

- Create games using only text and images, allowing for rapid and easy content
  creation by anyone
- Make it feel as though a player is walking through and exploring a book (text
  based adventure)
- Make worlds so big it takes months, maybe even years, to fully explore them
- Allow for character builds that are complex and unique (traits)
- Combat is highly customisable and tailored to specific encounters (rotation
  tables)
- Force the player to think before acting: wasting time is a bad idea
- The goal isn't shiny or the best equipment, it's defeating hard problems and
  being the best adventure the world as seen
- Taking actions costs a certain amount of time; you age as you move through
  the world and old age is a thing

These are the core tenants the engine will live by and aim to solve.

The lore (L) found throughout the world explains everything there is to be
understood about the world. It's how you understand the what, where, why, and
how of the world you're in. You need to study lore to open up the world map and
begin exploring. Lore tells you the skill rotations used by certain creatures
during combat (Beastology); how long it'll take to travel through a forest; or
how-to craft a particular spell or potion. Lore leads you to exploration.

Exploration (E) is how you progress your character through the world. It's also
how you find more lore to study. It's how you find foes to fight to get bigger
and stronger, level up, stash away gold, get better gear, and move on through
the world.

Exploring a dangerous world requires a good grasp of combat (C). Combat is, in
essence, a modified, automated game of Magic The Gathering. It involves
defining a rotation of skills and a set of reactions to certain events. Skills
are placed into a Rotation Table and Reaction Tables tell the game how ou want
to react to certain events. During a combat phase your rotation is executed in
order and your reactions trigger to events started by your enemies, who also
have skill rotation and reaction tables. Action Points (AP) are used to
constrict what and when you can execute an ability.

AP starts at one and crements by one each turn of combat (for both parties.)

Finally, time (T) is limited. As your characters studies lore, engages in
combat, and explores the world, you spend time. This isn't a new idea
(Fallout), but it'll really force the player to consider their actions and
think through what they're doing. As the character ages, their physical
attributes diminish but their wisdom and inntelligence increases. A character
can die of old age (somewhat random event) but magic can be used to prevent
this.

## Going deeper

Looking at each part of the engine in more detail might explain what I'm aiming
for and why.

### Lore Mastery

I love reading books and exploring worlds through them. Using your imagination
to build a world in your head is a wonderful thing. I also love it when a book
provides sketched maps of the areas it's talking to. I want my games to feel
like this.

The L in LECT is about making text-adventure games that make exploring the
world and map completion one of the primary ways to "win" the game. Having
explored all areas, uncovered all the lore, understood all the monsters, and
built a personal in-game library of books is one of the core principles behing
the engine. Patience and knowledge are rewarded heavily.

From a technical perspective Lore Mastery (LM) is used to uncover parts of the
world or explain something you can do within the universe. This done through
`grants`, which are pieces of meta data attached to items such as books,
scrolls, notes, noticeboards, and so on, which literally grant the player some
knowledge. An example might be:


```yaml --- type: book title: A Book of Example Spells Vol 6 author: The Great
Example Author date: 899BC

contents: # "chapters"
	- body: "At the end of the day... it's dark! So why not throw a nice juicy
	  fireball at something (or someone), set it on fire, and light the place
up a bit?" grants:
		- key: spell_fireball_level_2 conditions:
			- read_time: 120 # minutes; two hours
			- level: 30
	
	- body: "After setting someone on fire, you will likely need to peg it from
	  the coppers: why not teleport away? Perfect!" grants:
		- key: spell_teleport_level_2 conditions:
			- read_time: 300 # minutes; five hours
			- level: 35

	- body: "Now go forth and set things on fire! Just don't try and teleport
	  and fireball at the same time. Bad things will happen" grants:
		- key: trait_teleporting_fireball_madness conditions:
			- read_time: 510 # minutes; 8.5 hours
			- level: 30 ```

Or after reading a noticeboard, perhaps you become aware of a new town?

```yaml --- type: noticeboard title: Town Noticeboard contents:
	- body: "Liverpool is looking for people who can teleport! Good money. Come
	  to...." grants:
		- key: location_city_liverpool conditions:
			- level: 20
			- reputation_greater_than: 80 # > 80% with the targt location ```

Here we're seeing an example of the structure (which might change at this
point) of various items throughout a game world. These "items" can be placed
inside of a room and then explored or interacted with by a player. For example
the book can be piked up and read to learn new spells.

This kind of flexibility allows game masters to create very rich worlds with
restrictions and conditions that force players to come back later on (like
after reaching level 35 so they can learn the teleport spell, for example.)

Lore isn't restricted to locations or spells, however. It can be used to bestow
any knowledge on a player. Essentially a player can be told about anything in
the game and it's added to their library under the right catergory (beastology,
magic, maps, etc.) In the case of beastology, you can learn about an enemies
combat rotation (discussed below):

```yaml --- type: book title: Investigating Vampires Vol 3 # ...  contents:
	- body: "The programmer is a type of sugar vampire. They don't hunt and
	  consume human blood like most vampires. Instead they hunt (grab from the
fridge a free) sugary beverage and consume them on mass." grants:
		- key: beast_sugar_vampire conditions:
			- inventory_item_key: can_of_cuke ```

Which would yield something along these lines in the player's Beastology:

```yaml --- key: beast_sugar_vampire combat_rotations:
	- name: generic actions:
		- action_1
		- action_2 reactions:
		- reaction_4
		- reaction_3 conditions:
		- player_level_less_than: 30
		- player_class: mage ```

The more you read about Roy, um I mean "Sugar Vampires", the more about their
combat capabilities you know and the better you can plan ahead when facing them
in combat.

That's what Lore Mastery is about and that's why it's important to the game's
mechanics.
