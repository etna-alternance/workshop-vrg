---
title: Mapping tools - Quake Wiki
source: https://quakewiki.org/wiki/Mapping_tools
---

## Level Editor

**[TrenchBroom](https://trenchbroom.github.io/)**  -  the level editor used in this workshop. Cross-platform, actively maintained, purpose-built for Quake (and Quake-engine games).

Features: brush editing, entity placement, texture application, compile dialog (requires external compile tools  -  see below).

## Map Compile Tools

TrenchBroom does not bundle compile tools. The compile step (`.map` -> `.bsp`) requires **ericw-tools**, provided in `map_editor/ericw-tools-v0.18.1-*`.

Extract the archive for your platform, then configure TrenchBroom's compile dialog (**Run > Compile**) to point to the `qbsp`, `light`, and `vis` binaries inside it.

See `map_compiling.md` for what each tool does and when to run them.
