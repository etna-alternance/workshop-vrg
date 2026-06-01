---
title: Map metrics - Quake Wiki
source: https://quakewiki.org/wiki/Map_metrics
---

Each entity existing in the world of Quake, including player, always has certain dimensions assigned. This so called "bounding box" is distinct from an actual entity model. For level to not appear out of scale, and for player (and other entities) to be able to navigate inside of it properly, brushwork should always follow proper size conventions.

## Importance of physics

In Quake, entity bounding box also doubles as entity's hitbox.

It controls both physical behaviour of the entities (i.e. governs their movement and collisions) and also how player's weapons interact with the them (raycast damage tracing (from shotguns, thundergun), projectile collision (from nailgun nails, grenades and rockets), splash damage (from rockets and grenades) and environmental damage (from moving brushwork like doors, lifts and trains, and from environmental hazards like water, acid/slime and lava (for monsters only in some engines and mods)).

One of differentiating gameplay qualities of Quake is quite strong physicality of both the levels and the entity movement, giving levels and situations robust and realistic feeling.

The physics engine is relatively simple yet robust enough to allow players to treat levels like physics puzzles (especially when combined with advanced movement techniques like bunnyhopping, rocket jumping, grenade jumping and air control).

Most important physical object in the game is player, because of how their bounding box collides with rest of the level geometry determines where player will be allowed (or not) to go.

For good gameplay feel it helps to have level flow naturally and organically without unwanted hiccups, jumpy stairs, strange "stick" edges and crannies and other annoyances. Quake combat feels best when player is allowed to move fast and fluid.

Due to relatively competent air control, jumping puzzles can be fun, especially for advanced players, but not all players love them.

It also helps to design levels in such a way, that monsters can physically pursue the player too (AI of many monsters is well capable of pursuit and with some mapper's help even of some "advanced navigation" like jumping over ledges).

Thus physical dimensions are very important topics of Quake map design.

## Map limits

Most important limit in the whole game is, naturally, overall map size. There are four different limiting factors and two overall scenarios possible.

Main limiting factors are:

- coordinates storage format
- map formats
- algorithms employed
- and finally network protocol

General scenarios:

- player is using vanilla Quake engines: Quake, QuakeWorld
- player is using limit removing Quake port: FTEQW, Quakespasm Spiked...

### Vanilla Quake

In vanilla game the map is stored in BSP29 format which was targeted at medium level Pentium chip (e.g. around 90 Mhz) with medium amount of system memory. As such, limitations imposed on maps are quite severe (at least by today's standards).

While all BSP29 coordinates (of vertices for example) are expressed as floats during runtime internally (potentially allowing for very big maps), actual map allows only +/-32767u (u = in game units) per axis due to signed shorts (int16\_t) being used for nodes and leafs limits, and structure indexing is using only 16bit indexes and that and means only around 65535 objects of any kind, and in many cases much less.

These index limits can be exhausted very quickly (especially if mapper is not very careful with resource budgets and their economy), in many ways: very detailed geometry (running out of slots for map objects: vertices, edges or triangles/faces), very big flat surfaces (remember Quake 1 compilers usually subdivide surfaces automatically, to allow for lightmapping, and one surface quad subdivision requires quite a lot of resource objects to express: vertices, edges, triangles/faces), lightning (with animated lights, each face requires as many textures as the light style has light levels, more over rays from multiple animating lights hitting single face increase lightmap requirements exponentially due to combinatorial explosion caused by lightstyles for each light interacting) and so on.

Finally, player movement is severely limited further by network protocol and it's position/movement packets framing: in vanilla Quake the network layer is able to express player position only in measly range of +/-4000u, on any axis. If players gets near any of those limits on any axis, their position on that axis is "wrapped around". This means that player will "instantly teleport" to other side of the map (i.e. opposing minimum/maximum limit, depending on limit hit) while maintaining direction and acceleration they had when they hit the given limit.

The network protocol is always the limiting factor, even in single player mode, because the client/renderer part (what player sees) and server part (how player moves and collides) are the same between both single player and network play, only in SP mode, network communication is emulated using memory buffers. This client server design is described further here: xxx.

The limitation of +/-4000u (i.e. maps can be "only" 8000u wide) was probably chosen to conserve both emulated (SP) and real network code (MP) memory requirements and it also matched well with initial target hardware platform performance characteristics.

Vanilla engines are unable to load BSP2 maps due to binary format difference.

Conclusion:

- map size (hard limit, any axis): +/- 4000.0u
- level of map detail: very low.. low (basically how original Quake episodes look)

### Advanced engine ports

Few advanced Quake engine ports, especially limits removing ones like FTEQW and QSS, allow for much bigger maps due to implementing following important features:

- [BSP2 format](https://quakewiki.org/wiki/BSP2 "BSP2")
- new network protocols

Storage format for map geometry is again float, but now both on disk and in-memory. This allows for practically unlimited level geometry sizes.

Map structure indexing is now using 32bit indexes, thus effectively removing any realistic limit on how detailed the map can be (32bit number allows for 4 billions of object slots of any kind). This means map can be very big and very detailed which meshes much better with modern sensibilities. Resource economy is less critical.

Networking code is now capable of using so called \*\*bigcoords\*\* extension whis uses new coordinate coding allowing full range of float movement.

However although possibilities might now seem endless, with these changes, new limitations are exposed.

First and foremost float values lose the precision more the bigger the number they express is. Then, many game runtime data structures and algorithms were never intended to be run over datasets as big as when nearing BSP2 limits, so as one is reaching those limits, these algorithms might start to loose robustness, stability or fail otherwise.

QCVM, QuakeC Virtual Machine is practicularlly limited to floats sized between cca -4,194,304u - +4,194,304u for many vector and tracing operations.

Finally bigger indexes and other BSP2 structures means more disk and memory space consumed. Due to APIs used, practical physical.bsp map file size limitation is estimated to be around 4GB for BSP2 format.

As such, with BSP2 format, practical limits are much higher (virtually unlimited) and became much softer, and should one be nearing the maximums, it might lead to less obvious failures and bugs inside the engines.

So as long as one stays within reasonable bounds, anywhere between +/- 16 Ku ~ +/- 128 Ku, the engines are battle tested enough and will deal with any realistic map, but it is advised to not try to reach limits needlessly.

Keep in mind that many modern mods (and maps) use BSP2 format nowadays, and while not many of them are bigger than 8000u across, the playtimes often grow exponentionally as map volumes can now be filled with more brushes, thus more details, and thus more rooms and thus more paths between them, inflating the actual play experience considerably. It's not uncommon for new maps to be "size" of whole episode or even two of original game.

Advanced engines can load both vanilla and BSP2 maps. In case of running vanilla maps in advanced engines, extended limits still apply and protocols will switch on dynamically when needed.

Conclusion:

- map size:
	- hard limit, qcvm imposed, any axis: +/- 4194304u
		- soft limits, reasonable, any axis: +/- 8000u, +/- 16000u, +/- 32000u, +/- 64000u
- level of map detail: medium - very high (examples arcane dimensions etc.)
- bsp filesize on disk: anything > 256Mb can be considered insane