# Summary #

The function G\_GlobalSound was added in revision [r33](https://code.google.com/p/oax/source/detail?r=33).  This function allows for the server to tell all connected clients to play a sound.

In all honesty, the way sounds are played is pretty complex--local only sounds are triggered by clients directly, while most other sounds are triggered from events/player states/entity states contained in the snapshots sent out by the server.

This addition should significantly enhance the ability to add sounds to events in gameplay. It provides the "qagame" module direct control over what sounds to play, and when to play them.

The rationale for this feature is that, in all honesty, the gameplay experience can be significantly enhanced if certain gameplay events are announced globally--think of it like the TV/Radio announcer for a football (soccer) match, versus the announcer at the stadium. The TV/Radio announcer is much more engaging since he or she is actually describing what is happening, while the announcer at the stadium merely declares that an event has occurred.

There are some considerations however when employing this function--see the section below.


# How the Code Works #

```
void G_GlobalSound( int soundIndex )
{
    gentity_t  *te;    
        if( ( soundIndex == 0 ) || ( !soundIndex ) ) {
            #ifdef DEBUG
            G_Printf( "GlobalSound: Error, no soundIndex specified. Check your code!\n" );      
            #endif
            return;
        }    
        te = G_TempEntity( level.intermission_origin, EV_GLOBAL_SOUND );
        te->s.eventParm = soundIndex;
        te->r.svFlags |= SVF_BROADCAST;
}

```
  1. G\_GlobalSound first initializes a "game entity," "te."
  1. G\_GlobalSound aborts if there is a bad parameter passed to it. Continuing would cause the nasty crash described below.
  1. Since the function can really cause problems, I added an error message when compiling a "DEBUG" build.
  1. It then defines "te" as a temporary entity with the EV\_GLOBAL\_SOUND event.  Temp entities are used for creating events at particular positions.
  1. The code then defines the parameter for the EV\_GLOBAL\_SOUND event as the soundIndex passed to G\_GlobalSound.
  1. It then sets a broadcast flag for the entity, which is processed by the server executable on the next snapshot, where the server server executable will tell all the connected clients to play the sound.

# Usage #

The sound to be played must be assigned a "sound index" first. Then the call to G\_GlobalSound can be made.   To do this, initialize an `int` and then set it's value to the function G\_SoundIndex.  Then call G\_GlobalSound with the `int` as a parameter.
```
    int soundIndexReturned;

    //Some code blah blah blah
    
    soundIndexReturned = G_SoundIndex( "sound/misc/soundtobeplayed.wav" );
    G_GlobalSound( soundIndexReturned );
   
```
**Note:**
While G\_SoundIndex does return an `int`, it must **NOT** be nested as a parameter in G\_GlobalSound.  An example of doing this is:
```
   G_GlobalSound( G_SoundIndex( "sound/misc/soundtobeplayed.wav" ) );
```
Doing this can and will crash clients when they receive the instruction to play a sound that has not been indexed. It will leave them on their desktop with nothing more than an obscure "S\_FindName" error message.

You can call G\_SoundIndex with a reference to a "char" variable instead--however this provides for the possibility of the above client crash if you have not properly assigned the char a value.

Also, there is a limit to the maximum number of sounds a client can have, so this function must be used wisely.