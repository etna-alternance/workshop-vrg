---
title: Textures - Quake Wiki
source: https://quakewiki.org/wiki/Textures
---

![](https://quakewiki.org/w/images/9/99/Textures.png)

Some of Quake's Textures

Textures in Quake are [256 color](https://quakewiki.org/wiki/Quake_palette "Quake palette") images used in [Quake maps](https://quakewiki.org/w/index.php?title=Quake_maps&action=edit&redlink=1 "Quake maps (page does not exist)"). Each texture has a name of no more than 15 characters. Their dimensions are required to be a multiple of 16. Older hardware-rendered [engines](https://quakewiki.org/w/index.php?title=engine&action=edit&redlink=1 "engine (page does not exist)") would automatically resize textures to a [power of 2](http://en.wikipedia.org/wiki/Power_of_two), but most modern engines allow disabling this behavior if supported by the GPU. Textures are stored directly within [.bsp files](https://quakewiki.org/wiki/Quake_BSP_Format "Quake BSP Format") when used by Quake, or extracted, collected, and used in [.wad files](https://quakewiki.org/wiki/Texture_Wad "Texture Wad") by level designers.


## Special Textures

There are several special textures in Quake, which have properties defined either by the [QBSP](https://quakewiki.org/wiki/QBSP "QBSP") compiler or by the game [engine](https://quakewiki.org/wiki/Engines "Engines").

## Clip

![](https://quakewiki.org/w/images/e/e3/texture_clip.png)

Clip is a special texture, named "clip", which is invisible, yet blocks player and monster movement. Brushes must be fully textured with clip, and clip brushes do not seal the world from [leaks](https://quakewiki.org/w/index.php?title=leaks&action=edit&redlink=1 "leaks (page does not exist)"). Clip does not block weapon fire. Clip is commonly used to prevent the player from getting stuck on architectural details.

## Liquids

![](https://quakewiki.org/w/images/e/e8/texture_liquid.png)

Liquids are textures whose name is preceeded by the character "\*". By default, this means they are water in Quake and you may [swim](https://quakewiki.org/w/index.php?title=swim&action=edit&redlink=1 "swim (page does not exist)") in them. All faces of a brush must be of a single type of liquid texture, and they may not touch Sky textures. Their surface will also animate, and not block [Vis](https://quakewiki.org/wiki/Vis "Vis") on any modern compiler by default - meaning they can be made transparent by setting a water alpha value, either globally via console variables, or on a per-map basis via worldspawn fields.

A liquid with a name which starts with "\*slime" will be damaging slime, and a liquid with a name starting with "\*lava" will be even deadlier lava. When compiled by vis, liquids will play an automatic ambient sound. Beware that most versions of vis won't create sound for water liquids which do not begin with the name "\*water" or "\*04water". Modern vis programs allow you to turn off the creation of automatic ambient sounds.

Modern compilers also support skip versions of each liquid, so you can have placeholder textures named "\*waterskip", "\*lavaskip" and "\*slimeskip", that can still be used to define liquid volumes (even in conjunction with standard liquid textures), but will be invisible in the compiled map. See [Skip](#Skip) for more information.

- (when using replacement textures the "\*" prefix on the names of liquids inside a wad becomes an "#" in your texture replacement names.)

## Skies

![](https://quakewiki.org/w/images/e/e5/texture_sky.png)

Skies are textures whose name which start with the word "sky", and must be of dimensions 256x128. The texture is treated like two 128x128 textures, the right section used as a backdrop, and the left section used as an overlay with its black pixels transparent. Skies are displayed animated and full-bright, block player and monster movement, and 'swallow' weapon fire. Sky brushes do seal the world from leaks.

- Some engines (ex: Quakespasm) support sky textures of a different resolution (printing an error message in the console). Sky textures which are not 256x128 will not be animated correctly, so they should only be used if using a Quake II-style [skybox](https://quakewiki.org/w/index.php?title=skybox&action=edit&redlink=1 "skybox (page does not exist)"). Use [external textures](#External_Textures) if animated skies of a different resolution are desired.

## Animated textures

![](https://quakewiki.org/w/images/d/dc/texture_animate.png)

Simple animated textures with up to 10 frames can be used in Quake. Their name must begin with the character "+" and a number between 0-9. Quake will display a sequence beginning at "+0", "+1", etc, up to the highest number, and then loop back to "+0".

Animated textures may also switch to an alternate sequence if applied to some brush entities, such as [func\_wall](https://quakewiki.org/wiki/func_wall "func wall"), and [func\_button](https://quakewiki.org/wiki/func_button "func button") (doesn't work on [func\_door](https://quakewiki.org/wiki/func_door "func door")). When one of these entities is textured with an animated texture and is triggered, it will switch to an alternate sequence if it exists. These must be named the same as the original animated textures, except use "+a", "+b", up to "+j". You are not limited by the number of frames in the original animation, but you must begin at "+a".

An example of this is the button texture used in the base maps of Quake. "+0basebtn" and "+1basebtn" blink a red texture, and when the func\_button is used, it swaps to "+abasebtn".

## Skip

![](https://quakewiki.org/w/images/7/7c/texture_skip.png)

SKIP is a **nonstandard** special texture, used by modern QBSP compilers, but does not have any function in the stock Quake compilers as released by [id Software](https://quakewiki.org/wiki/id_Software "id Software"). Skip is a texture much like clip in that it is invisible, but skip's use is to remove an entire face from ever rendering, and a brush does not have to be fully textured in skip. The removed face remains solid and will block player and monster movement, as well as block weapon fire. In general, this is of little use on solid geometry, as Quake performs backside culling, but can be used on brush entities or "hacks" like windows to hide unwanted faces. `*waterskip`, `*lavaskip`, and `*slimeskip` textures exists as well, for use with liquid brushes.

- In ericw-tools, textures named NULL or BEVEL can also be used to not render a face.
- In ericw-tools, SKIP is normally solid, *except when combined with HINT*. This is different from other engines' compilers (Q2, HL1, etc.), wherein SKIP is always nonsolid.

## Alphatest Textures

![](https://quakewiki.org/w/images/f/ff/fence_texure.png)

Alphatest textures (sometimes called "fence" textures) are **nonstandard** special textures handled by the modern ericw-tools QBSP compiler and properly supported in some of the current quake engine ports. As the name implies these textures have parts that are alpha-masked so you can see through them. You can use these textures to make fences, spider webs, vines, bushes, icicles, trees, etc.

Alphatest textures are determined by having the 1st character in the texture name as "{", making any pixel using color index #255 (the pinkish one in the lower right-hand corner) of the [Quake palette](https://quakewiki.org/wiki/Quake_palette "Quake palette") to be rendered as transparent. For external TGAs, the alpha channel will be used instead (using an alpha clip threshold of 127). To support an alpha channel, TGA files must be in 32-bit format.

In supported engines, you can use them in any non-vis-blocking, non-geometry-culling brush entity, such as [func\_wall](https://quakewiki.org/wiki/func_wall "func wall"), [func\_illusionary](https://quakewiki.org/wiki/func_illusionary "func illusionary") or [func\_detail\_fence](https://quakewiki.org/wiki/func_detail#func_detail_vars "func detail"). Other [func\_detail](https://quakewiki.org/wiki/func_detail "func detail") variants may still cull away underlying geometry depending on the case, thus making likely you'll see the void through transparent texture areas.

(much of this article was rewritten from [http://www.celephais.net/stuff/texturefaq.htm](http://www.celephais.net/stuff/texturefaq.htm))

## External Textures

Some [source ports](https://quakewiki.org/wiki/Engines "Engines") enable the use of external textures by replacing the images supplied from the WAD with image files in the game directory. This allows for a much broader range of color, not limited by the standard palette of Quake.

## File format

While some engines are capable of replacing textures with many different image types, most engines specifically require an 24-bit or 32-bit [TGA](http://en.wikipedia.org/wiki/Truevision_TGA "wikipedia:Truevision TGA"), or an opaque 8-bit [PCX](http://en.wikipedia.org/wiki/PCX "wikipedia:PCX") (which does not have to adhere to the [quake palette](https://quakewiki.org/w/index.php?title=quake_palette&action=edit&redlink=1 "quake palette (page does not exist)")).

## Name format

In order for the engine to replace the correct texture from the WAD, the name of the texture and the image file must match; however, because of [limitations in the Windows file system](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#naming-conventions%7C), liquids texture replacements must be named using a different character. Instead of an asterisk being used, the number symbol "#" has to prefix the name.

## File location

These image files need to be placed within the same mod directory as the map you're trying to replace textures of (or the id1 folder if you want to replace it for all mods/maps). For replacements of world textures, place them inside of a directory called "textures" in order to be seen by the engine (e.g...\\Quake\\id1\\textures\\).

Certain source ports also allow for model and menu texture replacements, which are stored in much the same way, but in different directories. Model texture replacements should be placed within a directory called "progs" and menu replacements in a directory named "gfx".