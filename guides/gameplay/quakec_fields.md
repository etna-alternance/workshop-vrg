---
title: QuakeC Fields - Quake Wiki
source: https://quakewiki.org/wiki/QuakeC_Fields
---

Quake's fields are broken down into two main types: system fields and entity fields. When a field is declared, every entity in the game has their own version of that field. Valid field data types include `string`, `vector`, `float`, and `entity`. Function pointers are also allowed by specifying the return type and any parameters that need to be passed to it. The return type should be `void` if it doesn't return anything. Fields are declared via

```
.datatype variableName;
.returntype(datatype param1) functionPointer;
```

Note the `.` as declaring a variable without this will make it global instead of entity-specific. When setting a function pointer, only the name of the function is needed e.g. `entity.functionPointer = MyFunction;`. It can then be called like any other function by invoking the pointer.

System fields are fields defined within the engine itself and must be present for the game to work. These are always defined after the system global fields. The end of them is denoted by the `void end_sys_fields;` declaration. System fields must always be declared in the order defined within the vanilla QuakeC files as they are linked by memory offsets internally. Changing the order will break logic.

Entity fields are standard fields that have no internal linkage and can be defined freely anywhere. Declaring it will automatically give all entities access to their own version.

## System Fields

The following fields should be defined in the exact order of this list, otherwise memory offset errors can occur.

- *float* **modelindex**

The index for the entity's current model within the cache. Setting this to 0 will remove the entity's model. Otherwise this is best set via `setmodel()`.

- *vector* **absmin**

The world coordinate of the bottom left corner of the entity's axis-aligned bounding box. Both `setorigin()` and `setsize()` will set this. For BSP entities, `setmodel()` will also set this.

- *vector* **absmax**

The world coordinate of the top right corner of the entity's axis-aligned bounding box. Both `setorigin()` and `setsize()` will set this. For BSP entities, `setmodel()` will also set this.

- *float* **ltime**

The local time for the entity. This is used in place of the global **time** variable if the entity has the move type `MOVETYPE_PUSH` since BSP entities that get blocked will pause their timer.

- *float* **[movetype](https://quakewiki.org/wiki/Fields:Movetype "Fields:Movetype")**

The type of movement the entity has. There are special rules for what entities should have what move type.

- *float* **[solid](https://quakewiki.org/wiki/Fields:Solid "Fields:Solid")**

The type of collision the entity has. There are special rules for BSP entities regarding their **movetype**.

- *vector* **origin**

The current world coordinate of the entity. Should be set by `setorigin()` since it involves relinking the entity to the world.

- *vector* **oldorigin**

Used with `MOVETYPE_WALK` to determine if the entity is stuck when moving. Secret door entities also use this to record their spawn position.

- *vector* **velocity**

The movement direction and speed of the entity measured in map units/second.

- *vector* **angles**

The current direction as (pitch, yaw, roll) the entity's model is facing. Players use **v\_angle** for their camera direction. Note that positive pitch values point up and negative pitch values down within this field. If you wish to pass it directly to `makevectors()`, you should negate the pitch before doing so. BSP entities should not use this field as their bounding box will not be aligned to their orientation.

- *vector* **avelocity**

The angular velocity as (pitch, yaw, roll) of the entity measured in degrees/second. BSP entities should not use this field as their bounding box will not be aligned to their orientation.

- *vector* **punchangle**

The view angle offset as (pitch, yaw, roll) to apply to the player's camera e.g. weapon recoil.

- *string* **classname**

The type the entity is. Quake uses this to determine what spawn function to call for a given entity when it's first created while loading (the class name will match its spawn function's name).

- *string* **model**

The name of the entity's current model. Setting this to empty will remove the entity's model. Otherwise this is best set via `setmodel()`. For BSP entities, this field is automatically populated with the name of their internal BSP model on spawn.

- *float* **frame**

The current frame index for the entity's model.

- *float* **skin**

The current skin index for the entity's model.

- *float* **[effects](https://quakewiki.org/wiki/Fields:Effects "Fields:Effects")**

Flags that store which effects to apply to an entity e.g. muzzle flash.

- *vector* **mins**

The size of the entity pointing towards its bottom left. These should be negative values. Should be set by `setsize()` since it involves relinking the entity to the world. For BSP entities this is set by `setmodel()`.

- *vector* **maxs**

The size of the entity pointing towards its top right. These should be positive values. Should be set by `setsize()` since it involves relinking the entity to the world. For BSP entities this is set by `setmodel()`.

- *vector* **size**

The total size of the entity on all 3 axes. Should be set by `setsize()` since it involves relinking the entity to the world. For BSP entities this is set by `setmodel()`.

- *void()* **touch**

The function to run (if any) when a collision occurs with another entity, both on the collider and collidee respectively. Only runs if the entity is considered a form of solid. If an entity is a trigger only its `touch()` will be called.

- *void()* **use**

Unused.

- *void()* **think**

The next function to perform on the entity. Only gets called if **nextthink** is a positive value.

- *void()* **blocked**

Function called by BSP entities when they are unable to push an entity out of the way.

- *float* **nextthink**

The time stamp for when to perform the next `think()` action. If a non-positive number, does nothing. After an entity thinks this is automatically set back to 0. For standard entities **time** should be used to set the time stamp while for BSP entities the **ltime** field should be used instead.

- *entity* **groundentity**

The entity currently being stood on top of, if any. Used to denote standing on top of a BSP entity.

- *float* **health**

The current health of the entity. This should use rounded numbers as imprecisions can cause bugs at values less than 1.

- *float* **frags**

The number of kills the player currently has in PvP modes.

- *float* **weapon**

The item bit for the player's currently selected weapon.

- *string* **weaponmodel**

The name of the model to use for the player's HUD weapon.

- *float* **weaponframe**

The current frame index for the player's HUD weapon.

- *float* **currentammo**

The amount of ammo to display in the HUD for the player's currently selected weapon.

- *float* **ammo\_shells**

The amount of shells the entity currently has.

- *float* **ammo\_nails**

The amount of nails the entity currently has.

- *float* **ammo\_rockets**

The amount of rockets the entity currently has.

- *float* **ammo\_cells**

The amount of cells the entity currently has.

- *float* **[items](https://quakewiki.org/wiki/Fields:Items "Fields:Items")**

Tracks the items an entity currently has. Usage can vary depending on type of entity, but common usage is for players, backpacks, and locked doors. Note: For players, this has special interactions with the HUD.

- *float* **takedamage**

The type of damage the entity is capable of taking. Can be the following:
- `DAMAGE_NO`
- `DAMAGE_YES`
- `DAMAGE_AIM` (Signifies that the entity can be auto aimed at)

- *entity* **chain**

Used with `findradius()` to create a linked list of entities that were found. This should not be used outside this purpose or modified manually. Nested `findradius()` calls can break this functionality without special precautions.

- *float* **deadflag**

Used with players to denote their current respawn state. Can be the following:
- `DEAD_NO`
- `DEAD_DYING`
- `DEAD_DEAD`
- `DEAD_RESPAWNABLE`

- *vector* **view\_ofs**

The amount to shift from the origin of the entity to get its eye point.

- *float* **button0**

Boolean that determines if the fire button is pressed.

- *float* **button1**

Unused.

- *float* **button2**

Boolean that determines if the jump button is pressed.

- *float* **impulse**

The command a client is sending to the server. This is used for changing weapons and certain cheats. Only one impulse can be sent at a time per player.

- *float* **fixangle**

If set to `TRUE`, the player's camera angle is updated instantly based off their **angles** field. This is automatically cleared.

- *vector* **v\_angle**

The direction the player's camera is facing as (pitch, yaw, roll). Negative pitch values point up while positive pitch values point down.

- *float* **idealpitch**

If walking on a slope, the calculated pitch to align the player's camera with it. This is disabled if mouse input is active.

- *string* **netname**

The name of the entity, be it the player's name or a printable name for messages.

- *entity* **enemy**

For monsters, the entity it's currently chasing after. This is also the entity floating and swimming monsters will always try to align their height to.

- *float* **[flags](https://quakewiki.org/wiki/Fields:Flags "Fields:Flags")**

The flags for the entity.

- *float* **colormap**

The current color map index for the entity's model. This is mostly for player corpses and should match the player number the entity is mimicking.

- *float* **team**

What team the player is on in team-based PvP modes.

- *float* **max\_health**

The maximum amount a player can heal from standard health pickups.

- *float* **teleport\_time**

If greater than **time**, ignore movement inputs from the player. This is set immediately after teleporting to make sure the player can't run off into the abyss.

- *float* **armortype**

The fraction of damage to absorb. This only stores up to two decimal places by default.

- *float* **armorvalue**

How much armor the entity currently has.

- *float* **waterlevel**

The current liquid level of the entity. For players:
- `0` (Out of liquid)
- `1` (Below waist)
- `2` (Above waist)
- `3` (Above camera view height)

For other entities, this is only `0` (out of liquid) or `1` (in liquid).

- *float* **watertype**

The `CONTENT_*` type of the liquid the entity is standing in.

- *float* **ideal\_yaw**

For monsters, this is the yaw they want to turn towards.

- *float* **yaw\_speed**

How quickly the monster should turn towards **ideal\_yaw**. Measured in degrees per 0.1 seconds by default.

- *entity* **aiment**

Unused.

- *entity* **goalentity**

The entity monsters are trying to move towards, usually while patrolling. For floating and swimming monsters, they won't try to put themselves at level with it.

- *float* **spawnflags**

The flags set for the entity within the map editor itself. What spawn flags are available differs from entity type to entity type.

- *string* **target**

The **targetname** id that an entity will try and activate when it gets used. Different entity types have different use conditions.

- *string* **targetname**

The id of the entity for use in being activated.

- *float* **dmg\_take**

How much modified damage the player took on a given frame.

- *float* **dmg\_save**

How much damage was mitigated by the player's armor on a given frame.

- *entity* **dmg\_inflictor**

The last entity to deal damage to the player on a given frame.

- *entity* **owner**

Which entity is considered the owner of this entity. Entities will automatically pass through their **owner** instead of colliding with them.

- *vector* **movedir**

Used by various entity types to determine which way to move e.g. doors. Also used by the player when they're jumping out of a liquid.

- *string* **message**

What message to display when certain entity types are activated.

- *float* **sounds**

What type of sounds an entity uses. Often used for setting sound types on BSP entities from the map editor.

- *string* **noise**
- *string* **noise1**
- *string* **noise2**
- *string* **noise3**

Sounds that various BSP entities use to play audio during certain interactions.

## Entity Fields

These can be defined anywhere in any order. Removing or changing them isn't advised since maps use field names to determine what values to set, and any field can be arbitrarily set from the map editor. Modifying these could cause vanilla maps to break due to incorrect initializing.

### World Fields

- *float* **worldtype**

Used across various entity types to determine what type of level it is and what assets should be used e.g. keys.

- *string* **wad**

Unused.

### Map Entity Fields

- *string* **map**

Used by level changing entities to store what the next map to go to is.

- *float* **style**

The id of the light style layer to use for the light entity. Can be a value from \[0, 63\].

- *float* **light\_lev**

The intensity of the light entity.

- *float* **bubble\_count**

The number of bubbles for a bubble spawner to create.

- *string* **mdl**

Used by items to store their current model name so it can be reset when respawned.

- *float* **aflag**

The amount of ammo an ammo pickup gives.

- *float* **healamount**

The amount of health a health pickup restores.

- *float* **healtype**

The type of pickup a health item is. Can be one of the following:
- `0` (Small, 15 HP)
- `1` (Standard, 25 HP)
- `2` (Megahealth, 100 HP)

- *vector* **dest**

Unused.

### BSP Entity Fields

- *float* **speed**

Used by various entity types to determine how fast it moves towards its goal in map units/second.

- *vector* **mangle**

Used by certain entity types to store their map editor angles before resetting it to `VEC_ORIGIN`. This is often used to create directional movement.

- *float* **t\_width**

Used by secret door entities to calculate how far to move to get to their first destination. Also used as a time stamp for when the [Thunderbolt](https://quakewiki.org/wiki/Thunderbolt "Thunderbolt") can play its sound again.

- *float* **t\_length**

Used by secret door entities to calculate how far to move to get to their final destination.

- *vector* **dest1**

Used by secret door entities to record their first destination's position.

- *vector* **dest2**

Used by secret door entities to record their final destination's position.

- *float* **wait**

Used by various entity types to determine how long to wait before moving again e.g. buttons and doors. Also used by traps to determine their fire rate.

- *entity* **trigger\_field**

Stores the trigger a door uses to open itself.

- *string* **noise4**

Sound to play for locked doors.

- *float* **dmg**

Stores the amount of damage various entity types do when blocked or triggered. Also stores how much drowning damage to deal to the player.

- *void()* **think1**

The function to call when an entity reaches its movement or rotation destination.

- *vector* **finaldest**

The final calculated position of the entity's movement.

- *vector* **finalangle**

The final calculated angles of the entity's rotation. This shouldn't be used with BSP entities since their bounding box will not match their orientation.

- *float* **count**

Used by triggers to determine how many more times they must be activated.

- *float* **lip**

Distance in map units that doors and buttons stick out from the wall.

- *float* **state**

Stores the current state of various entity types. Can be one of the following:
- `STATE_TOP`
- `STATE_BOTTOM`
- `STATE_UP`
- `STATE_DOWN`

- *vector* **pos1**

Records the spawn position of various entity types.

- *vector* **pos2**

Records the destination position of various entity types.

### General Entity Fields

- *string* **killtarget**

The **targetname** id of the entities to remove from the map when activated. Contrary to its name, this will delete them and not kill them. This takes precedence over **target** by default.

- *float* **attack\_finished**

Time stamp for when the entity is allowed to attack again.

- *float* **pain\_finished**

Time stamp for when the entity can enter its pain state again.

- *float* **fly\_sound**

Time stamp for when the wind sound effect can be played again from an entity when it walks into a push trigger.

- *float* **delay**

If activated, wait this long before actually activating other entities.

- *float* **cnt**

Counter that tracks various behaviors e.g. monster refiring, Spawn jumping, and bubble splitting.

- *float* **distance**

Unused.

- *float* **volume**

Unused.

- *float* **hit\_z**

Unused.

### Monster Entity Fields

- *void()* **th\_stand**

The function to call when a monster starts to idle.

- *void()* **th\_walk**

The function to call when a monster starts walking towards its patrol points.

- *void()* **th\_run**

The function to call when a monster begins to chase its **enemy**.

- *void()* **th\_missile**

The function to call if a monster has a ranged attack.

- *void()* **th\_melee**

The function to call if a monster has a melee attack.

- *void(entity attacker, float damage)* **th\_pain**

The function to call when the monster is damaged.

- *void()* **th\_die**

The function to call when a monster dies.

- *entity* **oldenemy**

Stores the last valid enemy a monster had before switching targets.

- *float* **lefty**

Boolean used by strafing monsters to determine which direction they're strafing (if `TRUE`, moves left).

- *float* **search\_time**

Time stamp used in co-op modes as a cool down for monsters looking for a new target to attack.

- *float* **attack\_state**

The current attacking state of the monster. Can be one of the following:
- `AS_STRAIGHT`
- `AS_SLIDING` (Currently strafing)
- `AS_MISSILE`
- `AS_MELEE`

- *float* **pausetime**

Time stamp for when a monster can start walking towards its patrol points.

- *entity* **movetarget**

The patrol point entity a monster is trying to walk towards.

- *float* **waitmin**

Time stamp for when [Scrags](https://quakewiki.org/wiki/Scrag "Scrag") can play their idle sound.

- *float* **inpain**

Used by [Zombies](https://quakewiki.org/wiki/Zombie "Zombie") to determine what pain state they're in. Can be one of the following:
- `0` (No pain state)
- `1` (Flinching)
- `2` (Knocked down)

- *float* **waitmax**

Unused.

### Player Entity Fields

- *float* **walkframe**

The current frame of the player's idle and running animations.

- *float* **invincible\_finished**

Time stamp for when the [Pentagram of Protection](https://quakewiki.org/wiki/Pentagram_of_Protection "Pentagram of Protection") powerup wears off.

- *float* **invincible\_time**

Time stamp that controls the sound and screen flash from the Pentagram of Protection wearing off.

- *float* **invincible\_sound**

Time stamp for when the protection sound can be played again when taking damage.

- *float* **invisible\_finished**

Time stamp for when the [Ring of Shadows](https://quakewiki.org/wiki/Ring_of_Shadows "Ring of Shadows") powerup wears off.

- *float* **invisible\_time**

Time stamp that controls the sound and screen flash from the Ring of Shadows wearing off.

- *float* **invisible\_sound**

Time stamp for when the Ring's whispering sound effect is played.

- *float* **super\_damage\_finished**

Time stamp for when the [Quad Damage](https://quakewiki.org/wiki/Quad_Damage "Quad Damage") powerup wears off.

- *float* **super\_time**

Time stamp that controls the sound and screen flash from the Quad Damage wearing off.

- *float* **super\_sound**

Time stamp for when the Quad firing sound effect can be played again.

- *float* **radsuit\_finished**

Time stamp for when the [Biosuit](https://quakewiki.org/wiki/Biosuit "Biosuit") powerup wears off.

- *float* **rad\_time**

Time stamp that controls the sound and screen flash from the Biosuit wearing off.

- *float* **axhitme**

Signifies that the player was hit by another player's axe that frame.

- *float* **show\_hostile**

If greater than **time**, nearby monsters will wake up without needing to see the player.

- *float* **jump\_flag**

Stores the player's z velocity when not on the ground.

- *float* **swim\_flag**

Time stamp for when the swimming sound should be played again while jumping underwater.

- *float* **air\_finished**

Time stamp for when the player runs out of air when under a liquid and begins to drown.

- *string* **deathtype**

Used to determine if the player fell to their death by setting it to "falling".

- *float* **dmgtime**

Time stamp for when a harmful liquid can damage a player again.