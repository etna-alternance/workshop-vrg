# To clone it **IMPORTANT!!!**

```sh
git pull --recurse-submodules
```

# Introduction

Game development is hard. Mark my words: it's an unforgiving and ungrateful job.

When developing a game alone, the learning curve is so steep that most people give up before they even truly begin.

The reason is simple: it's a multi-domain project involving far more work than meets the eye.

If you aren't afraid of hard work, you're thirsty for creativity and knowledge, and you're still attracted to game development after hearing what I've told you, then I'd like to welcome you among us Lunatics!

# Workshop Objectives

- Learn the existence of the different domains in GD (Game Development)
- Dive into specific a specific domain of GD
- A small mod from any domain (Gameplay, Presentation or Story). The goal isn't to make a masterpiece, but to discover the tools and process behind video games, to get a small peek at Game Development.

*(all in 3h30... ;-;)*

# How and Why?

Modding (easier to build from something than from scratch):
- Solid and prebuilt foundation in every domains
- Students can focus on a particular aspect of GD

*Guides and Tools in each domain are at your disposition in this folder to achieve this workshop objectives more easily :D*

# Phases

1. Application (2h30)
2. Showcase (1h)

# Roles & Domains
*"Game Design Trinity": It's mostly about Presentation, Story and Gameplay.*

- Presentation -> Design:
    - Game Designer
    - Level Designer
    - Narrative Designer
    - UI/UX Designer
- Story -> Art:
    - 3D Artist
    - Texture Artist
    - Material Artist
    - Concept Artist
    - Animator / Rigger
    - VFX Artist
    - SFX Artist
    - Composer
- Gameplay -> Programming:
    - Gameplay Programmer
    - Engine Programmer
    - Graphics Programmer
    - AI Programmer
    - Network Programmer
    - Tools Programmer
    - Audio Engineer

*Checkout [roles](guides/roles.md) for more details*

# Prerequisites

**Install this before doing anything else.** Follow the guide for your platform:

- **Windows 64-bit** — `prerequisites/win64/README.md` — install the C++ runtime redistributables
- **Linux x86-64** — `prerequisites/linux-x64.md` — Qt 6.7+ required for TrenchBroom
- **macOS** — `prerequisites/macos.md` — Gatekeeper bypass required for all tools

# Tools and Folder Structure

prerequisites/      -> install before anything else  
compiler/           -> for Gameplay (Win64, Linux-x64, MacOS-Universal)  
asset_editor/       -> for Story (Win64, Linux-x64, MacOS-x64, MacOS-arm64)  
map_editor/         -> for Presentation (Win64, Linux-x64, MacOS-x64, MacOS-arm64)  
engine/             -> to run the game (Win64, Linux-x64, MacOS-arm)  
quake-src/          -> the game source code  
quake/              -> the game files  
guides/             -> helpful resources from each domain to help you during your modding journey :D  
    gameplay/       -> you'll learn Gameplay Programming  
    presentation/   -> you'll learn Mapping  
    story/          -> you'll learn how to make Assets  

To begin, start with the README.md inside a domain folder. Good Luck! :D