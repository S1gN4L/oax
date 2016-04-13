# How to Use the OpenArena Server Administration System #

## General Command Usage ##
Using the OpenArena Admin system is pretty uniform.  All the Admin commands are preceded by an exclamation mark. If g\_adminParseSay is enabled, they can be executed from either the normal console window, the "say:" line, or the "say\_team:" line.  If it is disabled, the command must be entered from the player-admin's console. For a complete command listing, please see the [Admin Command Reference Page.](Admin_Commands.md)

For example, if the admin Leilol wanted to "slap" player SharpestTool for railing his team's flag carrier into the void on a space map, she could bring up the "say:" chat prompt with the "t" key, and enter: "!slap SharpestTool 50 Stop Doing that."

Upon doing that, 50 hp damage would be done to the player SharpestTool, and he would receive a "center-printed" message across his screen that would say "Leilol slapped you because: Stop Doing that."

Using the !help command will display a list of admin commands available to the admin, and when used in conjunction with another command will display the target command's usage.  eg: !help ban, will display how to use the !ban command.

If an admin attempts to execute a command he/she does not have the appropriate level or flags for, he/she will receive the following error message "!(command): permission denied!" where (command) is the name of the command they were attempting to execute.  The failed attempt will be logged in the "admin.log" file as well.

---


## General Behavior of the OpenArena Admin System ##

The OpenArena Admin System reads the "admin.dat" file each time the "qagame" module is loaded by the server.   This means, it is read automatically each time a map is loaded, or the game is restarted.  It will also read the "admin.dat" file when the !readconfig command is executed by the appropriate admin.

External or "manual" changes to the "admin.dat" will only take affect when the "admin.dat" file is read by the OpenArena Admin System.  To be sure changes take affect, it is important that the !readconfig command is executed after any changes have been made.

Once the "admin.dat" file has been read, all the associated `[levels]`, `[admins]`, `[commands]`, `[bans]`, and `[warnings]` are loaded into the server's memory.

When an admin command is entered by a player, it is first processed by the server, and upon finding the preceeding exclamation mark, it is first verified that it is a valid admin command.  Then the Admin System verifies the player has the necessary admin privileges to execute it.  Finally, the command is checked for proper usage. Upon reaching this point, the command is then executed.

When commands are executed or attempted they are logged to the "admin.log" file along with the player executing/attempting the command.


