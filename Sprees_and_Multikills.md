# Overview #

Killing Sprees, Death Sprees, and Multi-kills are new features introduced in revision [Revision 49](http://code.google.com/p/oax/source/detail?r=49). These features add a level of customization which significantly enhances the multiplayer experience of OpenArena.  See each page below for more information on how to enable, customize, and work with these new features.

## General Behavior ##

Killing Spree and Death Spree announcements occur along an interval specified by the server.  When a player attains a number of kills or deaths which is a multiple of that interval, a sound is played and a message is broadcast to the other players in the game.

Multi-kills are meant to replace the stock "Excellent" award sound.  A sound and message can be specified for the "number" of kills a player achieves. While the award sound is replaced, the actual award, is not.  This means that the "Excellent" sprites will still be shown above the player's head to the other players, and the award will still be added to the player's historical award count (as visible in the UI). Please see the configuration page for more information.


## "Infinite" Sprees / Multi-kills ##

One important behavior worth mentioning is that Killing Sprees, Death Sprees, and Multikills are infinitely awarded, regardless of the number defined by the server operator.  When a player goes over largest level defined by the server, the server will merely repeat the sound and message for the largest level defined. ( See each configuration page for limits on the number of levels that can be defined.)

The way this works for Killing / Death Sprees, is that they are defined in the code to occur at fixed intervals.  When a player's number of consecutive kills and deaths reaches a multiple of that interval, it searches for the level defined by that interval.  If there is no level defined, the largest Killing / Death Spree is repeated over again.

While multikills are defined on the server in terms of "number of kills" and not by an interval's level, they exhibit similar behavior because they were designed to take the place of the "Excellent" award sound. (For more information see the [Configuring Multi-kills page](MultKill_Config.md) )  If a player goes over the largest number of kills as defined by server, the largest multi-kill is played over again.

This behavior was created with future gameplay design considerations in mind.

---

## Pages ##

**[Enabling Sprees and Multi-kills](Enabling_Sprees_MultiKills.md)**

**[Configuring Killing / Death Sprees](Configuring_Sprees.md)**

**[Configuring Multi-kills](MultKill_Config.md)**

### Reference ###

The Settings File

Building Custom pk3's

NOTE: While these features can also be enabled in Single-Player mode, they were designed for multi-player server customization and thus are not enabled by default!!

---
