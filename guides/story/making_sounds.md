---
title: Making sounds - Quake Wiki
source: https://quakewiki.org/wiki/Making_sounds
---

## Sound File Formats

Most sounds in the original Quake are [mono](https://en.wikipedia.org/wiki/Monaural) [WAV files](https://en.wikipedia.org/wiki/WAV) with a sample rate of 11025 Hz and a bit depth of 8. This is usually referred to as "11kHz 8-bit mono". You can use other sample rates, but they may be resampled to 11kHz depending on the end-user's engine and configuration.

All engines load WAVs as 16bit, unless the user sets the [loadas8bit](https://quakewiki.org/w/index.php?title=loadas8bit&action=edit&redlink=1 "loadas8bit (page does not exist)") cvar (which basically exists only for running in DOS with only 8MB RAM, something that's generally not gonna happen nowadays...).

## Looping Sounds

Looping sounds can be created in the Quake engine by adding a cue point at the start of the WAV file, for example with [LoopAuditioner](https://loopauditioneer.sourceforge.io/).

Engines that support Vorbis or other formats for non-music sounds also usually make the [ambientsound](https://quakewiki.org/wiki/ambientsound "ambientsound") builtin force looping (from the start of the file, when there's no explicit cue point set).