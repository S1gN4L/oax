# Introduction #

Multi-kills are designed to replace the stock "Excellent" award.   When a player acheives a multikill a sound/message will be broadcast globally to all other players about the event.  A sprite will be drawn above his/her head for others to see, but the icon that would normally flash on the screen of the player being awarded "Excellent" will be absent.

That said, you should have read first how to [Enable Sprees and Multikills](Enabling_Sprees_MultiKills.md). That page should give you the information needed regarding the cvar, `g_altExcellent` and the general behavior associated with it.

NOTE: While the in-game behavior is different, a player will still receive credit for having acheived the "Excellent" reward in his/her historical statistics.

# Details #

## Considerations/Known Issues ##
  1. Multikills were designed to be a replacement to the stock "Excellent" sounds.  As a result it's probably best to space the multi-kills at intervals of 1.
  1. Turning on Multi-kills mid-match, without having them defined at the start of the match will result in no sound being played for the client/player who attains the "Excellent" award.   This behavior is by design...see more here `[placeholder, will put link here later].`