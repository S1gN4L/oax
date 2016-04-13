# Introduction #

In order to allow tools to read and understand the log files it is important to be consistent in the way we write game events to the log file. Generally a line in the log file consist of a time stamp (auto added), the event type (like CTF or Item), a colon, a fixed number of integers explaining the event/sub event/client numbers and such. At last another colon followed by a human readable message.

# Here are the events implemented so far: #

```
award syntax: Award: #1 #2: S1 gained the S2 award
#1 and S1 are the client number and nick
#2 and S2 are the award types, corresponding to the following table:
Code:

#2 | S2
----------------
 0 | GAUNTLET
 1 | Excellent
 2 | Impressive
 3 | Defense
 4 | Capture
 5 | Assist


CTF syntax: CTF: #1 #2 #3: S1 got the S2 flag! / S1 captured the S2 flag! / The S2 flag has returned! / S1 returned the S2 flag / S1 fragged S2's flag carrier
#1 and S1 are the client number and nick, when there is no client involved #1 = -1
#2 and S2 are the team number and name
#3 is the event number, corresponding to the following table:
Code:

#3 | Event description
----------------------
 0 | Flag is taken
 1 | Flag is captured
 2 | Flag is returned
 3 | Flagcarrier got killed


1FCTF syntax: 1FCTF: #1 #2 #3: S1 got the S2 flag! / S1 captured the flag! / The flag has returned! / S1 fragged S2's flag carrier
#1 and S1 are the client number and nick, when there is no client involved #1 = -1
#2 and S2 are the team number and name
#3 is the event number, corresponding to the following table:
Code:

#3 | Event description
----------------------
 0 | Flag is taken
 1 | Flag is captured
 2 | Flag is returned
 3 | Flagcarrier got killed

HARVESTER syntax: HARVESTER: #1 #2 #3 #4 #5: S1 brought in #5 skulls
#1 client number
#2 team number that is scored for, if scored
#3 Event number, see table
#4 client number of enemy. Used for event 1
#5 number of points

#3 | Event description
----------------------
 0 | Skulls captured
 1 | Skull carrier killed 
 2 | Friendly skull picked up/destroyed
 3 | Enemy skull picked up

OVERLOAD syntax: to be decided

ELIMINATION syntax: ELIMINATION: #1 #2 #3: Round number S1 started! / S2 wins round S1  by eleminating the enemy team! /
 S2 wins round S1 due to more survivors! / S2 wins round S1 due to more health left! / Round S1 was a draw!
#1 and S1 are the round number
#2 and S2 is the winning team or -1 if not interresting.
#3 is the event number, corresponding to the following table:
Code:

#3 | Event description
----------------------
 0 | Round started
 1 | Win by elimination
 2 | Win by survivors
 3 | Win by health
 4 | Draw


CTF_ELIMINATION syntax: CTF_ELIMINATION: #1 #2 #3 #4: S2 got the S3 flag! / S2 captured the S3 flag! /
 The S3 flag has returned! / S2 returned the S3 flag / S2 fragged S3's flag carrier /
 The round has stated, S3 team is attacking! / S3 defended the flag! / S3 eliminated the enemy team!
#1 and S1 are the round number
#2 and S2 are the client number and nick, when there is no client involved #2 = -1
#3 and S3 are the team number and name
#4 is the event number, corresponding to the following table:
Code:

#4 | Event description
----------------------
 0 | Flag is taken
 1 | Flag is captured
 2 | Flag is returned
 3 | Flagcarrier got killed
 4 | Round has stated
 5 | Win by defending
 6 | Win by elimination
 7 | Win by survivors
 8 | Win by health
 9 | Draw

OBELISK/OVERLOAD syntax: OBELISK: #1 #2 #3 #4: S1 destroyed the enemy obelisk / S1 dealt #4 damage to the enemy obelisk
#1 and S1 are the client number and name
#2 is the team
#3 is the event (see table)
#4 damage to the obelisk (event 1)

#3 | Event description
----------------------
 1 | Obelisk took damage
 3 | Obelisk destroyed
 
HARVESTER syntax: #1 #2 #3 #4 #5: S1 fragged S4 (S2) who had #5 skulls. 
#1 and S1 are the client number and name
#2 and S2 are the team number and name
#3 is the event (see table)
#4 and S4 are the client number and name
#5 is number of skulls

#3 | Event description
----------------------
 0 | Scores
 1 | Fragged skull carrier
 2 | Skull destroyed
 3 | Skull picked up


LMS syntax: LMS: #1 #2 #3: Round S1 stated / S2 eliminated!
#1 and S1 are the round number
#2 and S2 are the client number and nick, when there is no client involved #2 = -1
#3 is the event number, corresponding to the following table:
Code:

#3 | Event description
----------------------
 0 | Round stated
 1 | Eliminated

DD syntax: DD: #1 #2 #3: S1 took point A for S2! / S1 took point B for S2! / S2 scores!
#1 and S1 are the client number and nick, when there is no client involved #1 = -1
#2 and S2 are the team number and name
#3 is the event number, corresponding to the following table:
Code:

#3 | Event description
----------------------
 0 | Point A is taken
 1 | Point B is taken
 2 | Scores

DOM syntax: DOM: #1 #2 #3 #4: S1 took control of point S2
#1 and S1 are the client number and nick. 
#2 and S2 are the number and name of the point taken. For event 1 this is the number of points 
#3 is the event number, following the table below.
#4 is the team number.
 
#3 | Event description
----------------------
 0 | Point taken
 1 | Team scores 
 
```