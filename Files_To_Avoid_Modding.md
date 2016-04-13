## Summary ##
I'll post files that should not be changed here. There are three reasons for not changing certain files:

  1. The file is shared with the engine code and unless the engine code is changed simultaneously as well, any changes to the code inside will have no effect.
  1. The file is shared with the engine code and unless the engine code is changed simultaneously as well, changes to the file **CRASH THE GAME!!!**
  1. Changing the file will necessitate changing a file that falls into one of the above categories.

## List of Files ##

  * ### qcommon/q\_shared.h ###
Changing declarations in this file can/will really confuse the server-especially any of the typedefs, structs, or enums.  Expect to crash the game when modding this as much of it is basically an API for the engine.
  * ### qcommon/q\_shared.c ###
Since all of q\_shared.c's declarations are contained in q\_shared.h, modding this file can necessitate changing q\_shared.h.  It's probably best to leave it alone. If you feel that something belongs in this file it properly belongs in bg\_libs.c instead.
  * ### client/keycodes.h ###
Shared with the engine. For reference only.
  * ### botlib/ ###
Engine only. For reference only.