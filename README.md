# To clone it **IMPORTANT!!!**

```sh
git pull --recurse-submodules
git lfs fetch --all
```

# Introduction

Game development is hard. Mark my words: it's an unforgiving and ungrateful job.

When developing a game alone, the learning curve is so steep that most people give up before they even truly begin.

The reason is simple: it's a multi-domain project involving far more work than meets the eye.

If you aren't afraid of hard work, you're thirsty for creativity and knowledge, and you're still attracted to game development after hearing what I've told you, then I'd like to welcome you among us lunatics...

# Workshop Objectives
*(all in 3h30... ;-;)*

- Learn the existence of the different domains in GD (Game Development) -> Checkout [roles](guides/roles.md)
- Dive into specific a specific domain of GD -> [Gameplay](guides/gameplay/README.md), [Presentation](guides/presentation/README.md), [Story](guides/story/README.md).
- Make a mod in a domain you like

# Workshop (hidden) Objective

The goal isn't to make a masterpiece, nor is it to make a working mod (even if that would be nice :D). The goal is to discover the tools and process behind game development, and as told just up there, it's a multi-domain project.

**Meaning you could potentially learn something (by learning Game Development) that could help you improve/push further your projects in a totally different domain.**

So try to see what kind of possiblities this domain could offer you and that you could use to your advantage, even if you aren't interested in Game Development (which is perfectly understandable ~~skill issue~~).

For those still interested despite everything I've told, completing this workshop in every domain will make you able to make any kind game from A to Z (these are foundations).

# How and Why?

Modding (it's easier to build from something than from scratch):
- Solid and prebuilt foundation in every domains
- Students can focus on a particular aspect of GD

# Prerequisites

**Install this before doing anything else.** Follow the guide for your platform:

- [Windows 64-bit](prerequisites/win64.md)
- [Linux x86-64](prerequisites/linux-x64.md)
- [macOS](prerequisites/macos.md)

# Tools and Folder Structure

```
prerequisites/      -> install before anything else  
tools/
    compiler/       -> for Gameplay (Win64, Linux-x64, MacOS-Universal)  
    asset_editor/   -> for Story (Win64, Linux-x64, MacOS-x64, MacOS-arm64)  
    map_editor/     -> for Presentation (Win64, Linux-x64, MacOS-x64, MacOS-arm64)  
    engine/         -> to run the game (Win64, Linux-x64, MacOS-arm)  
    quake-src/      -> the game source code  
    quake/          -> the game files  

guides/             -> helpful resources from each domain to help you during your modding journey :D  
    gameplay/       -> you'll learn Gameplay Programming  
    presentation/   -> you'll learn Mapping  
    story/          -> you'll learn how to make Assets  
```