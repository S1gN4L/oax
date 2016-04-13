# Summary (Problem) #

In the original Quake 3/ioQuake3 source code, dynamic memory allocation is not possible within the "game logic" modules when they are built as "Quake Virtual Machines" (QVM) or .qvm files.  Without going into details of how, the ISO standard functions "malloc" and "free" are not supported in the QVM build process.  The original programmers did include  solutions to allocate memory (such as G\_Alloc from g\_mem.c in the "qagame" module), but not ones to free it.

The effect of this is a severe limit on what features can be added to the "game logic" modules. For example: If a modification to "qagame" requires the use of "malloc"/"free" the programmer is either forced to compile the mod in native binary format (which negates the pure server distribution capability), or use "G\_Alloc" in place of "malloc" (which risks "qagame" running out of memory since there is no way to free it.)

Memory heavy features such as loading player specific profiles, or incorporating advanced scripting systems are not possible or unfeasible under the original Quake 3/ioQuake 3 source.

# Details (OAX Solution) #

Well, first and foremost, it is not originally "our solution."  The code is pretty much directly copied from the Tremulous project (under the GPL V2 of course!).  It is the original work of Tim Angus (according to notes in the code).  We have merely integrated it into the source code for OpenArena.

Programmers wishing to use "malloc"/"free" can now use "BG\_Alloc"/"BG\_Free" instead (and build their mods as QVM's).  They are defined in the file bg\_alloc.c, and declared in bg\_public.h. Their use is identical to that of "malloc"/"free" and for all intensive purposes are directly equivalent.

So far, all references to "G\_Alloc" have been painlessly converted, and the function "Svcmd\_GameMem\_f" was copied over to bg\_alloc.c.  The file "g\_mem.c" exists in the OAX source for reference purposes only-it is completely removed from the compile/build process.

This will provide OAX and others the ability to build some pretty advanced features for OpenArena (or with very minor modification Quake 3).