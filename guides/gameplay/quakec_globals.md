---
title: QuakeC Globals - Quake Wiki
source: https://quakewiki.org/wiki/QuakeC_Globals
---

Globals are variables that aren't entity specific and can be accessed from anywhere at any time. Much like fields, they're broken down into system globals and QuakeC globals. Valid global data types include `string`, `vector`, `float`, and `entity`. Globals are declared via:

```
datatype globalName;
```

System globals are globals defined within the engine itself and must be present for the game to work. These are always defined before anything else. The end of them is denoted by the `void end_sys_globals;` declaration. System globals must always be declared in the order defined within the vanilla QuakeC files as they are linked by memory offsets internally. Changing the order will break logic.

QuakeC globals are standard globals that have no internal linkage and can be defined freely anywhere.

Note that these are not stored between maps and will be reset upon changing levels.

## System Globals

The following globals should be defined in the exact order of this list, otherwise memory offset errors can occur.

- *entity* **self**

The entity that the physics frame is currently processing.

- *entity* **other**

If a collision is occurring, this is the entity **self** is colliding with. This should only be used from `touch()` functions.

- *entity* **world**

The default world entity. This entity's fields cannot be written to directly and it is considered null in conditional checks.

- *float* **time**

The current game time in seconds.

- *float* **frametime**

The difference between the previous physics frame and the current one in seconds.

- *float* **force\_retouch**

If greater than 0, relinks all entities into the world. Useful for getting entities to touch newly created triggers. This should be set to 2 to properly reset everything since setting it to 1 will only relink entities starting from the current **self** onward.

- *string* **mapname**

The name of the current map e.g. start, e2m1, etc.

- *float* **deathmatch**

If non-zero, PvP is enabled. If set to 2, uses the classic deathmatch rules.

- *float* **coop**

If non-zero, co-op is enabled.

- *float* **teamplay**

If non-zero while PvP is active, team PvP is enabled. If set to 1, friendly fire is disabled.

- *float* **serverflags**

Tracks the state of the game across the entire session. This doesn't get reset between level changes. The first 4 bits are reserved for the runes with each bit corresponding to its respective episode e.g. episode 1 is the first bit. If this is non-zero when going back to the start map, the player's inventory will be cleared.

- *float* **total\_secrets**

The total secret count for the current map.

- *float* **total\_monsters**

The total monster count for the current map.

- *float* **found\_secrets**

How many secrets have been found in the current map.

- *float* **killed\_monsters**

How many monsters have been killed in the current map.

Parms store information about each player when moving between levels. Players have their own set of parms, but the globals act as an interface for setting them. These can be changed to however the modder wants to encode information, but below is how they're handled by default.

- *float* **parm1**

Stores the player's **items** field minus any keys and power ups.

- *float* **parm2**

Stores the player's health. This is capped between 50 and 100.

- *float* **parm3**

Stores the amount of armor the player has.

- *float* **parm4**

Stores the amount of shells the player has. This has a minimum amount of 25.

- *float* **parm5**

Stores the amount of nails the player has.

- *float* **parm6**

Stores the amount of rockets the player has.

- *float* **parm7**

Stores the amount of cells the player has.

- *float* **parm8**

Stores the player's **weapon** field.

- *float* **parm9**

Stores the player's armor damage reduction multiplied by 100 to give two decimal places of accuracy (decimal places beyond this get discarded).

- *float* **parm10**
- *float* **parm11**
- *float* **parm12**
- *float* **parm13**
- *float* **parm14**
- *float* **parm15**
- *float* **parm16**

Unused

The following are used by `makevectors()` to store the local axes that the function generates from the passed angles.

- *vector* **v\_forward**

The facing direction of the passed angles.

- *vector* **v\_up**

The direction pointing 90 degrees up from the facing direction of the passed angles.

- *vector* **v\_right**

The direction pointing 90 degrees to the right of the facing direction of the passed angles.

The following are used by `traceline()` to pass information from the function to QuakeC.

- *float* **trace\_allsolid**

If `TRUE`, the trace was stuck entirely in solids.

- *float* **trace\_startsolid**

If `TRUE`, the trace started inside of a solid.

- *float* **trace\_fraction**

The fraction of the total distance the trace traveled before stopping. Ranges from \[0, 1\].

- *vector* **trace\_endpos**

The position the trace stopped.

- *vector* **trace\_plane\_normal**

The normal of the plane that the trace hit.

- *float* **trace\_plane\_dist**

The distance from the world origin of the plane that the trace hit. This is d in the plane equation ax + by + cz + d = 0.

- *entity* **trace\_ent**

The entity that the trace hit.

- *float* **trace\_inopen**

If `TRUE`, the trace traveled through open air.

- *float* **trace\_inwater**

If `TRUE`, the trace traveled through a liquid.

- *entity* **msg\_entity**

When sending a network message to a specific player via `MSG_ONE`, this is the player the message is sent to.

Below are a special set of global functions the engine calls. These have no internal definitions so the function body must be defined somewhere in QuakeC to work. As such, their functionality is entirely customizable.

- *void()* **main**

Unused.

- *void()* **StartFrame**

Called at the start of every physics frame before anything else is processed.

- *void()* **PlayerPreThink**

Called before the player's physics is ran.

- *void()* **PlayerPostThink**

Called after the player's physics is ran.

- *void()* **ClientKill**

Called when the player kills themselves via the console command.

- *void()* **ClientConnect**

Called when a player joins the game, either for the first time or from changing levels.

- *void()* **PutClientInServer**

Called when a player is set to spawn or respawn.

- *void()* **ClientDisconnect**

Called when a player leaves the game, either from disconnecting or changing levels.

- *void()* **SetNewParms**

Sets the default parms for the player when they join the game for the first time or when respawning in deathmatch.

- *void()* **SetChangeParms**

Called when the player is about to change levels and their parms need to be set so they can be decoded when joining the new map.

## QuakeC Globals

These can be defined anywhere in any order. Since they can't be set from the map editor they're free to be changed and removed, but doing so may break saves so exercise caution. It may be better to just deprecate them to keep save compatibility.

### World Globals

- *string* **string\_null**

Null string. This differs from empty strings in that it's not considered a valid string in conditional checks while empty strings are.

- *float* **skill**

The current difficulty of the map. Can be one of the following:
- `0` (Easy)
- `1` (Normal)
- `2` (Hard)
- `3` (Nightmare)

- *float* **framecount**

The total number of physics frames the server has processed.

- *float* **gameover**

If `TRUE`, the server is changing levels and players should not be considered fully disconnected.

- *string* **nextmap**

Stores the name of the next map to go to when changing levels e.g. start, e4m4, etc.

- *float* **intermission\_running**

Stores the type of intermission cutscene currently being played. Can be one of the following:
- `1` (Stats screen)
- `2` (End of episode text crawl)
- `3` (All runes collected text crawl)

- *float* **intermission\_exittime**

Stores the time stamp for when the intermission should end and change levels.

- *entity* **lastspawn**

Stores the last multiplayer spawn point found in order to cycle through them when spawning players in.

- *entity* **bodyque\_head**

Stores a queue of entities to track player corpses. Tracks up to 4 corpses by default.

### Map Entity Globals

- *entity* **s**

Tracks the last teleport fog entity that was spawned.

### General Entity Globals

- *entity* **activator**

The entity that's considered the activator when calling `SUB_UseTargets()`.

- *entity* **damage\_attacker**

The source of the attack when an entity takes damage.

- *entity* **newmis**

Set by `launch_spike()` to store the newly created projectile entity.

- *entity* **multi\_ent**

When firing a shotgun attack, stores the entity that's currently being damaged by tracers.

- *float* **multi\_damage**

When firing a shotgun attack, stores the total amount of damage to apply to **multi\_ent** after the tracers are done or when hitting a different entity.

### Monster Entity Globals

- *float* **movedist**

When attempting to move, stores how far the current monster is trying to travel in map units.

- *entity* **sight\_entity**

The monster that just woke up from finding a valid target. This is used so other monsters can see it and check to wake up themselves.

- *float* **sight\_entity\_time**

The time stamp for when the monster woke up from finding a valid target. In order for **sight\_entity** to be valid other monsters must have seen it within 0.1 seconds.

- *float* **enemy\_vis**

If `TRUE`, the current monster was able to see its enemy while chasing.

- *float* **enemy\_infront**

If `TRUE`, the current monster's enemy was in front of the direction it's facing while chasing.

- *float* **enemy\_range**

Determines how far away the current monster's enemy is while chasing. Can be one of the following:
- `RANGE_MELEE` (within 120 map units)
- `RANGE_NEAR` (within 500 map units)
- `RANGE_MID` (within 1000 map units)
- `RANGE_FAR` (1000+ map units)

- *float* **enemy\_yaw**

The yaw that points towards the current monster's enemy while chasing.

- *float* **hknight\_type**

Determines what type of melee attack Death Knights will perform. Can be one of the following:
- `0` (Slice attack)
- `1` (Overhead attack)
- `2` (Long combo slice attack)

- *entity* **le1**

When fighting Chthon, stores the first pillar that lowers in the lightning trap.

- *entity* **le2**

When fighting Chthon, stores the second pillar that lowers in the lightning trap.

- *float* **lightning\_end**

When fighting Chthon, stores the time stamp for when the pillars in the lightning trap should raise back up after being activated.

- *entity* **shub**

Stores a pointer to Shub-Niggurath so the finale cutscene can play out correctly.

### Player Entity Globals

- *float* **modelindex\_eyes**

Stores the model index in the cache for the eyes when the player is invisible.

- *float* **modelindex\_player**

Stores the model index in the cache for the player.