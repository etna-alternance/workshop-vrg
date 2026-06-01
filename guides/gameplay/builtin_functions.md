---
title: List of builtin functions
source: https://quakewiki.org/wiki/List_of_builtin_functions
---

Builtin functions are functions in QuakeC that perform a callback to a function within the engine itself. They're declared by creating a function prototype and assigning it to an index within the internal builtin table.

```
returntype(datatype param1) functionname = #[index];
```

For instance, `makevectors()` is defined as `void(vector ang) makevectors = #1;` since it sits at index 1.

## Vanilla Builtins

All functions below are vanilla Quake builtins supported by Ironwail.

| # | Function |
|---|----------|
| 1 | [makevectors](https://quakewiki.org/wiki/makevectors) |
| 2 | [setorigin](https://quakewiki.org/wiki/setorigin) |
| 3 | [setmodel](https://quakewiki.org/wiki/setmodel) |
| 4 | [setsize](https://quakewiki.org/wiki/setsize) |
| 6 | [break](https://quakewiki.org/wiki/break) |
| 7 | [random](https://quakewiki.org/wiki/random) |
| 8 | [sound](https://quakewiki.org/wiki/sound) |
| 9 | [normalize](https://quakewiki.org/wiki/normalize) |
| 10 | [error](https://quakewiki.org/wiki/error) |
| 11 | [objerror](https://quakewiki.org/wiki/objerror) |
| 12 | [vlen](https://quakewiki.org/wiki/vlen) |
| 13 | [vectoyaw](https://quakewiki.org/wiki/vectoyaw) |
| 14 | [spawn](https://quakewiki.org/wiki/spawn_(function)) |
| 15 | [remove](https://quakewiki.org/wiki/remove) |
| 16 | [traceline](https://quakewiki.org/wiki/traceline) |
| 17 | [checkclient](https://quakewiki.org/wiki/checkclient) |
| 18 | [find](https://quakewiki.org/wiki/find) |
| 19 | [precache_sound](https://quakewiki.org/wiki/precache_sound) |
| 20 | [precache_model](https://quakewiki.org/wiki/precache_model) |
| 21 | [stuffcmd](https://quakewiki.org/wiki/stuffcmd) |
| 22 | [findradius](https://quakewiki.org/wiki/findradius) |
| 23 | [bprint](https://quakewiki.org/wiki/bprint) |
| 24 | [sprint](https://quakewiki.org/wiki/sprint) |
| 25 | [dprint](https://quakewiki.org/wiki/dprint) |
| 26 | [ftos](https://quakewiki.org/wiki/ftos) |
| 27 | [vtos](https://quakewiki.org/wiki/vtos) |
| 28 | [coredump](https://quakewiki.org/wiki/coredump) |
| 29 | [traceon](https://quakewiki.org/wiki/traceon) |
| 30 | [traceoff](https://quakewiki.org/wiki/traceoff) |
| 31 | [eprint](https://quakewiki.org/wiki/eprint) |
| 32 | [walkmove](https://quakewiki.org/wiki/walkmove) |
| 34 | [droptofloor](https://quakewiki.org/wiki/droptofloor) |
| 35 | [lightstyle](https://quakewiki.org/wiki/lightstyle) |
| 36 | [rint](https://quakewiki.org/wiki/rint) |
| 37 | [floor](https://quakewiki.org/wiki/floor) |
| 38 | [ceil](https://quakewiki.org/wiki/ceil) |
| 40 | [checkbottom](https://quakewiki.org/wiki/checkbottom) |
| 41 | [pointcontents](https://quakewiki.org/wiki/pointcontents) |
| 43 | [fabs](https://quakewiki.org/wiki/fabs) |
| 44 | [aim](https://quakewiki.org/wiki/aim) |
| 45 | [cvar](https://quakewiki.org/wiki/cvar) |
| 46 | [localcmd](https://quakewiki.org/wiki/localcmd) |
| 47 | [nextent](https://quakewiki.org/wiki/nextent) |
| 48 | [particle](https://quakewiki.org/wiki/particle) |
| 49 | [ChangeYaw](https://quakewiki.org/wiki/ChangeYaw) |
| 51 | [vectoangles](https://quakewiki.org/wiki/vectoangles) |
| 52 | [WriteByte](https://quakewiki.org/wiki/WriteByte) |
| 53 | [WriteChar](https://quakewiki.org/wiki/WriteChar) |
| 54 | [WriteShort](https://quakewiki.org/wiki/WriteShort) |
| 55 | [WriteLong](https://quakewiki.org/wiki/WriteLong) |
| 56 | [WriteCoord](https://quakewiki.org/wiki/WriteCoord) |
| 57 | [WriteAngle](https://quakewiki.org/wiki/WriteAngle) |
| 58 | [WriteString](https://quakewiki.org/wiki/WriteString) |
| 59 | [WriteEntity](https://quakewiki.org/wiki/WriteEntity) |
| 67 | [movetogoal](https://quakewiki.org/wiki/movetogoal) |
| 68 | [precache_file](https://quakewiki.org/wiki/precache_file) |
| 69 | [makestatic](https://quakewiki.org/wiki/makestatic) |
| 70 | [changelevel](https://quakewiki.org/wiki/changelevel) |
| 72 | [cvar_set](https://quakewiki.org/wiki/cvar_set) |
| 73 | [centerprint](https://quakewiki.org/wiki/centerprint) |
| 74 | [ambientsound](https://quakewiki.org/wiki/ambientsound) |
| 75 | [precache_model2](https://quakewiki.org/wiki/precache_model2) |
| 76 | [precache_sound2](https://quakewiki.org/wiki/precache_sound2) |
| 77 | [precache_file2](https://quakewiki.org/wiki/precache_file2) |
| 78 | [setspawnparms](https://quakewiki.org/wiki/setspawnparms) |
