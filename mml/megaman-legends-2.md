---
description: Overview of Legends 2 files and games
---

# Megaman Legends 2

Megaman Legends 2 was the follow up to Megaman Legends 1 that was released for the Playstation console in 2000. It was later re-released in Japan for the Playstation portable. And the game also has a Japanese only Windows release.

### Versions

* Playstation (English)
* Playstation (Japanese)
* Playstation Portable (Japanese)
* Windows XP (Japanese)

We can look at each one of the three versions to see which ones will give us easier access to the files inside and for debugging features. The PSX version is likely going to be the easiest to work with as I am familiar with the save state format form PCSX-reloaded.&#x20;

The Playstation portable and PC versions might be interesting for different reasons. As looking into these might help with looking for options to port the English text over from the game to make these accessible to the community. And I get more familiar with PPSSPP's web socket debugging, this might offer a possibility of being easier to work with.&#x20;

If the PC version offers the ability to work into Windowed mode, then that might be a possibility as far as being able to multitask with other tools. One problem with the Windows is the installer uses Shift-JIS, which causes the characters to be unreadable for the installer. So it might be worth tracking down a Japanese laptop with Windows XP if it can't be emulated in Virtual Box.&#x20;

For the Playstation portable, release. I think this might be the exact Japanese release of the game with a few changes made to the binary for the widescreen to work. Not sure if the game takes advantage of the expanded memory and extra video memory. If it does it might solve one of my largest issues with working with the Playstation version which is mapping textures from files to their locations in video memory.&#x20;

It seems like one of the first steps should be getting my hands on each one of the versions and then comparing all of the files for each one of the versions to see how they stack up. From there I can look into the different options for which of the files offers the best approach for reverse engineering the files.&#x20;
