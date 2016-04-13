# Introduction #

To make the game more rewarding to players who face go online a challenge system has been introduced. The word challenge is because the system in time should be extended with goals like 'Get 100 excelent awards for bronze medal' etc. Currently the system is called 'Statistics' because no such challenges exist.

The challenge system is meant to aspire players to play against human players and should only record positive challenges: Challenges to be prod of or challenges that encourage good sportsmanship. A 'judge' award could go to the player who killed more players from the top half of the scoreboard than the bottom half. Maybe a challenge for joining the weakest team and still win.

# Details #


The challenges is defined in game/challenges.h and are given numbers in the range from 0 to 2047.

The challenges should be divided into categories like 1XX is gametype awards. 2XX is weapon kills 3XX is ingame awards. And so on.

The challenge system may record invisible stats like firstblood and last kill etc. Loosing a match but having killed the winner the most might not show ingame but in the players stats the fact might be forever recorded.

Challenges should only be awarded against human opponents.
```
if(!level.hadBots) //There has not been any bots
        ChallengeMessage(attacker,AWARD_EXCELLENT);
```
Is an example of how to check that the challenge is against a human opponent.

The command to add a challenge is
```
void ChallengeMessage(gentity_t *ent, int challenge)
```
This will add 1 to the challenge in the client `*`ent. You cannot give negative challenges.

An unfortunate weakness of the system is that an evil server can ruin the statistics by sending fake challenges messages to ruin the experience of the players... that is just to bad. I still prefer the server to handle the challenges.

Challenges are also written to the log file, so that 3rd party tools can parse them for display on webpages