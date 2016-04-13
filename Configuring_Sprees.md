# Overview #

First, if you are reading this page without having first read how to enable Killing Sprees and Death Sprees, click on the Previous Page link below.

Now that you have read how to enable Killing Sprees and Death Sprees, you are ready to configure them.  The first premise that must be understood is Killing Sprees and Death Sprees will occur at the same fixed interval specified by the cvar "g\_spreeDiv." See the previous page [here.](Enabling_Sprees_MultiKills.md)

For example, at the default setting of "5," Killing Sprees and Death Sprees, will occur at every 5 kills and 5 deaths. Each interval can be defined by a "level" in the settings file of the server, beginning at 1, and ending at 32.  Why 32? See below...

---


# Details #

As described above, the server operator defines an interval that the Killing Sprees and Death Sprees are to occur at.  They define each "level" in the settings file. The following must happen for Killing / Death Sprees to be properly configured.
  1. A plain text file which matches the name specified by the "g\_sprees" cvar must be created.
  1. The above file must be placed in the "baseoa" sub-directory of the OpenArena "working directory." See the [previous page](Enabling_Sprees_Multikills.md) for details.

---


### Killing Sprees ###
```
[kspree]
level = 1
printpos = 2
message = [n] is on a killing spree!!! ( [k] kills!!! )
sound = sound/misc/killingspree.wav
```
Killing sprees are denoted with the `[kspree]` tag as described above.

The "level" attribute is the level at which to print the message and play the sound.

The "printpos" attribute instructs the server the "position" in which to "print" the "message".   Setting the "printpos" to "1" will "center print" the message across the screen, "2" will have it printed to the "chat" stream.  It's probably not wise to set every message to "center print" as it will become annoying/distracting for players if killing sprees are common on the server. ( or if "g\_spreeDiv" is set to a low number like "2" )

The "message" attribute is the message for the server to print when the specified Killing Spree occurs.   The text `[n]` and `[k]` are placeholders in the message. `[n]` will be replaced by the player's name. `[k]` will be replaced by the number of kills for that level.

The "sound" attribute is the sound for the server to play when the specified Killing Spree occurs.  For the sound to be played properly, the path must be made in accordance with the Quake 3/OpenArena file system structure, see the page Building pk3's for more information.

So, in summation for the example written above, when "g\_spreeDiv" is set to 5, and the player "Leilol" acheives 5 consecutive kills without dying, Leilol has acheived the first level (level = 1). This means the following will happen.

  1. The "message" "Leilol is on a killing spree!!! ( 5 kills !!! ) will be displayed to all players in the "chat" block at the upper left hand side of the screen.
  1. The "sound" killingspree.wav will be played to all players.

#### Configuration Rules: ####
  1. The maximum number of killing sprees which the server can read is 32. It will throw error messages or possibly even crash if more than that are defined ( Do you really even need more? ).
  1. The "message" can be no more than 150 characters, ( with the name and kill number placeholders replaced ). Longer messages will be truncated, or even ignored.
  1. Server operators can specify text to be formatted to a certain color in the same manner they would set a player name or format chat text.
  1. If the "printpos" is not set to either "1" or "2", the message will not be printed.
  1. Sound files must be 22khz wav's or "ogg" format.  See the [ioQuake3 home page ](http://ioquake3.org) for more information on enabling support for "ogg" sound files.
  1. Setting g\_spreeDiv to either 0 or 1 will have the server revert back to the default behavior of using 5 for the "spree interval."  Also, it will not correct the cvar, instead it will merely ignore the cvar, revert to the default behavior, and continue printing console error messages on every map/game load. This behavior is by design so some of the newbie server owners out there won't crash their servers.
  1. Killing Sprees above 99 kills in length will be truncated.  If this happens in regular online play, WOWWW!!! Post it on the OpenArena forums, however we still won't change it. :-)

---


### Death Sprees ###

Death Sprees are configured identically to killing sprees except they use the `[dspree]` tag instead.
```
[dspree]
level = 1
printpos = 2
message = [n] is a total NOOBBBB!!! ( [k] straight deaths!!! )
sound = sound/misc/noob.wav
```

So again, if the cvar "g\_spreeDiv" is set to "5," and the player "SharpestTool" dies 5 times in a row without a kill, he will trigger the first "level" and the following will happen.

  1. The "message" "SharpestTool is a total NOOBBBB!!! ( 5 straight deaths!!! )" will be displayed to all players in the "chat" block at the upper left side of the screen.
  1. The "sound" "noob.wav" will be played to all players.

Death Sprees also have the same configuration rules as Killing Sprees.

---


Next Page:[Configuring Mult-kills](MultKill_Config.md)

Previous Page: [Enabling Sprees/Multi-kills](Enabling_Sprees_MultiKills.md)

