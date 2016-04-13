# Introduction #

Per revision "[R24](https://code.google.com/p/oax/source/detail?r=24)" console command handling has been significantly changed.  ClientCommand (g\_cmds.c) and ConsoleCommand (g\_svcmds.c) now employ a loop structure by which to check the command the user/player enters against a table.  If it successfully finds a match, the loop breaks and a validation check is made, based on the parameters specified in the table.  If this validation check is successful, either ClientCommand or ConsoleCommand, then calls the associated command handler specified inside the corresponding table.

This provides significant "modularity" to adding/maintaining console commands, and provides increased flexibility to the "child" command handlers.  Since all "child" command handlers which require "arguments" now must be written with the ability to trap those arguments themselves, "commands" having similar functionality can now be called from the same handler.

# Details #
To successfully add a command, either as a "ClientCommand" (g\_cmds.c) or a ConsoleCommand (g\_svcmds.c) the following needs to happen.
  1. Functions to be called from ClientCommand (g\_cmds.c) must have, and only have the parameter `gentity_t *ent`. eg:
```
void functionToBeCalled ( gentity_t *ent )
{
  //Code to run
}
```
  1. Functions being called from ConsoleCommand (g\_svcmds.c) must have no parameters. eg:
```
void functionToBeCalled ( void )
{
  //Code to run
}
```
  1. If the function is contained in another code file, it must be declared in a header file, either "g\_local.h" or a header file referenced by an `#include` in "g\_local.h"
  1. If the function is in the same file, it must be placed above/before either the "ClientCommand" (g\_cmds.c) or ConsoleCommand (g\_svcmds.c) and preferably be defined as `static`.
  1. An entry must be made in the corresponding array (`commands_t cmd[]` for a "ClientCommand" in g\_cmds.c, and `svcmds[]` for a ConsoleCommand in g\_svccmds.c). See below for the way the two command tables/arrays are structured.
  1. All fields for the array/table must be entered--if they are to be "null," "0" or "NULL" should be entered.

Getting a command to work properly is another story and completely up to the person writing the command. Here are some considerations:
  1. Should the command only run if entered from the server? If so, the command must be placed/processed under g\_svcmds.c  Adding the command into g\_cmds.c will otherwise give any/all players access to it.
  1. Does the command need to process "arguments?" If so, inside the function, "trap\_Argv" can be called in order to parse them.
  1. Are there certain conditions when the command should be ignored? See the command flags below.


## ClientCommand (in g\_cmds.c) ##
### Command Table/Array Structure ###
```
typedef struct
{
    char    *cmdName;
    int     cmdFlags;
    void    ( *cmdHandler )( gentity_t *ent );
} commands_t;
```

  1. The "cmdName" must be entered into the "cmd" array with quotation marks. It is a literal string.
  1. The "cmdHandler" is the name of the function to be called. Only the name of the function should be entered--`( gentity_t *ent )` must not trail the name!!!
  1. "ent" is the entity which entered the command.  This is the only parameter common to all commands entered into the console which are a "ClientCommand."

The "cmdFlags" are below.
### "cmdFlags" (from g\_local.h) ###
```
#define CMD_CHEAT           0x0001 // is a cheat command
#define CMD_CHEAT_TEAM      0x0002 // is a cheat/exploit when used on a team
#define CMD_MESSAGE         0x0004 // sends message to others (skip when muted)
#define CMD_TEAM            0x0008 // must be on a team
#define CMD_NOTEAM          0x0010 // must not be on a team
#define CMD_RED             0x0020 // must be on the red team (useless right now)
#define CMD_BLUE            0x0040 // must be on the blue team (useless right now)
#define CMD_LIVING          0x0080 // must be alive to use this command
#define CMD_INTERMISSION    0x0100 // the command can be used during intermission
```

Note: I am not going to analyze the validation inside ClientCommand, there are too many details and doing so is just rewriting the code in plain language! :) That said, here are some considerations.
  1. If a command is to be enabled during intermission, it must be flagged with "CMD\_INTERMISSION" as the stock validation check ignores commands when the game is in intermission if they are not flagged as such.
  1. Cheat commands are checked against the value for the cvar "g\_cheats" and not sv\_cheats. (Sorry if I am stating the obvious for experienced Q3-based game modders.)

## ConsoleCommand (in g\_svcmds.c) ##
### Command Table/Array Structure ###
```
struct
{
  char      *cmd;
  qboolean  dedicated; //if it has to be entered from a dedicated server
  void      ( *function )( void );
} svcmds[ ] //code continues directly...blah blah blah
```

  1. "cmd" must be entered into the table inside of quotes as it is a literal string.
  1. "dedicated," if set to "qtrue" means the command will only run if the server is dedicated (cvar g\_dedicated set to either "1" or "2").
  1. "function" is the name of the function to be called by ConsoleCommand. Only the name should be entered--`(void)` must not trail the name!!!
