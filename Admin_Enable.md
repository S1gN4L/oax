# Enabling/Configuring OpenArena Server Administration #

## Overview ##
Enabling and configuring the OpenArena admin system is fairly simple and straightfoward for out-of-the box functionality. It only requires the Server Owner/Operator to have knowledge of where his/her OpenArena "Working Directory" is located on his/her server.

---


## Details ##
For out-of-the-box functionality this checklist can be used to enable the OpenArena Admin System.
  1. Create an empty plain-text file named "admin.dat."
  1. Place the empty "admin.dat" file in the working "baseoa" sub-directory of OpenArena.
  1. Set the appropriate CVAR's. (See Below)
  1. Start your server.  Review the console output to make sure there is a line under the "game initialization" section that says "!readconfig: loaded 0 levels, 0 admins, 0 bans, 0 commands, 0 warnings."
  1. Delegate the highest Admin level from the "Server Console," using the !setlevel command (Syntax: !setlevel `<player> <adminlevel>` ). For example, if the player Sago007 is the player you want to make your highest admin, you would type !setlevel Sago007 5 (where Sago007 is the player you want to make Admin, and level 5 is the level of Admin privileges you want to give him).  This can either be done directly, for a dedicated server, or using RCON.
  1. Your "Head Admin" can now delegate lesser or equal admin privileges from within the game, using the !setlevel command either from his/her own console, the "say:" line, or the "say\_team:" line.  He/she can now also execute the various Admin commands at his/her disposal.
  1. If you desire different privileges than the default configuration, you should NOW edit the "admin.dat" file directly, setting your appropriate levels and flags accordingly. (See "Admin.Dat File" below.)  After editing the "Admin.Dat" file, be sure the !readconfig command is executed by the appropriate admin.

---


### CVAR's ###
  * **g\_admin:** Set's the name of the "admin.dat" file, which the Server looks for on startup, writing Kicks, Bans, and Warnings as well as storing admin levels. The default is "admin.dat."
  * **g\_adminLog:**  Set's the name of the "admin.log" file. This file keeps track of all the Admin actions which take place on the server.   Default is "admin.log"  This should NOT be set to your Game Log file as doing so will create errors and corrupted log data.
  * **g\_adminParseSay:** Allows for the "say:" and "say\_team:" lines and commands to parse Admin commands.  "1" enables, "0" disables.   Default is "1," enabled.
  * **g\_adminNameProtect:** Does not allow other players to rename themselves to player names used by server admins.  Setting this to "1" enables the protection, "0" disables it.   Default is "1," enabled.  We highly recommend Server Operators leave this CVAR set to default to avoid having unruly players getting your own Admins kicked, banned, or muted, etc.
  * **g\_adminTempBan:** This is the standard time an Admin can "kick" players for.  If a longer kick is necessary, use the !ban  command instead of the !kick command.  The number must be followed by a time unit of measurement (WITHOUT SPACES!!!)  Acceptable units are "s" for seconds, "m" for minutes, "h" for hours, "d" for days, and "w" for weeks.  Default is "2m" meaning 2 minutes.
  * **g\_adminMaxBan:**  This is the maximum time an Admin can "ban" players for.  "Banning" a player for longer will require the use of the "server Console" or delegating the "Can Permanently Ban" privilege directly to an appropriate admin.  The default is "2w" meaning 2 weeks.  The acceptable units of measurement are the same for g\_adminMaxBan as they are for g\_adminTempBan.
  * **g\_maxWarnings:**  This is the maximum number of "Warnings" a player can receive before being "auto-kicked" by the Server.  Default is "3."
  * **g\_warningExpire:** This is the amount of time (in seconds) it takes for a "Warning" to wear off.  Default is 3600, meaning 1 hour.

---


### The "admin.dat" File ###
Once you have your CVAR's set, you can begin editing your "admin.dat" file.   Server Operators should make sure their game servers' directory structures have been secured properly to unwanted access to this critical file.

The "admin.dat" file is essentially a storage file for all the necessary information for use of the OpenArena Admin System.  It stores the admin levels defined by the Server Operator, the admin levels for each admin, custom Command definitions, Players Bans, Player Warnings, and Player Kicks.

IMPORTANT: IF THIS FILE IS DELETED OR BECOMES CORRUPTED THE SERVER WILL LOSE ALL INFORMATION AND REVERT TO DEFAULT SETTINGS! **BE SURE TO BACK-UP THIS FILE OFTEN!!!**

Now that all the scary stuff is out of the way, let's take a look at the "admin.dat" file.  (For a visual sample open this link in a new window [here.](Admin_File.md))

The various sections of the "admin.dat" file are denoted by bracket tags. `[level]` corresponds to an admin level, `[admin]` for an individual admin, `[command]` for a custom command, `[ban]` for kicks/bans, and `[warning]` for player warnings.  For more information on the `[command]` tag please see the appropriate section [here.](Admin_Cust_Cmds.md)

#### `[level]` Tags ####
The most important component of the "admin.dat" file are the admin levels, specified with the `[level]` tags. They describe the basic permissions associated with each player.  Contained within each `[level]` is a "level" attribute, a "name" attribute, and a "flags" attribute.

The "level" attribute is a number the Admin System uses to identify the `[level]` as unique.   It is important that no duplicates are created when editing the "admin.dat" file by hand as it could cause unpredictable behavior.

**Using the !setlevel command on a player assigns the specified "level" to the player.**

The "name" attribute is what will appear on screen in OpenArena when either an !admintest, !listplayers, or !listadmins command is executed.  Color characters entered as part of the "name" attribute will show on screen as well.   "Name" attributes are limited in length to 32 characters.

The "flags" attribute is the most important attribute to the `[level]` tag as it defines the commands, and privledges afforded to admins who have been assigned that level.   The "asterisk" character denotes the highest level of authority available.   For a list of flags, see the [list of Admin Commands and flags.](Admin_Commands.md)

#### `[admin]` Tags ####
If assigning Administrative permissions and privileges through the use of !setlevel is not flexible enough, specific permissions and privileges can be assigned to individual admins manually through modifying the appropriate `[admin]` tag for that player.

An `[admin]` tag has the following attributes, "name," "guid," "level," and "flags."  The name is a mere friendly identifier in game and used to make the "admin.dat" file understandable when reading.

The "guid" attribute is the actual unique identifier (if you have to ask, you should probably not be reading this). Since it's created completely programatically, it should never be edited by hand. **LEAVE THE GUID ATTRIBUTE ALONE!**

The "level" attribute represents the admin level the admin has been assigned to.  It corresponds to the appropriate `[level]` tag.  While changing it manually to adjust an admin's privileges or permissions, it is probably best to do so using the !setlevel command in game.

The "flags" attribute represents individual commands, or permissions which the admin has access to in addition to their assigned admin level.  For a list of flags, see the [list of Admin Commands and flags.](Admin_Commands.md)

---


### Considerations/Stuff To Avoid Doing ###
  1. If you only have one "Head Admin," it is very unwise to have him/her perform a !setlevel command on him/herself.  Doing this erroneously can result in a loss of his/her admin privileges and will necessitate the use of the !setlevel command from the "Server Console" directly to restore lost privileges.
  1. The "Server Console" has ultimate Admin authority.  This means you should keep your RCON password as private as possible, being sure not to divulge it to untrusted players.  It is also advisable to make sure your Server's directory structure has been secured/permissioned properly.
  1. Don't !setlevel to every player around.  The maximum number of admins you can have is 1024.  The admin system defaults all unknown players to level 0 and does not count a level 0 player as an admin.  If you wish to delegate certain features such as !time, !help, or !admintest to level 0 players, edit the "admin.dat." file directly and set the appropriate command "flags," for level 0.