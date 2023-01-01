# PlayStation

## Approaches

* Save States
* Edit Files / CD Image
* Read Assembly

## Emulators

At this point a Playstation emulator can be run on a toaster, or a remotely fast potato of a computer. The following is a list of the most common Playstation emulators.&#x20;

* PCSXR
* ePSXe
* no$PSX
* Duck Station
* RetroArch

### PCSXR

Available On: Linux and Windows (sort of)

PCSXR is the easiest emulator to work with as it is open source. That means if you need to look at the code, or make changes you can. While you may not need to, the ability to do this was what allowed me to unpack the save state format to be able to export and see the save state format.&#x20;

This emulator works really well on Linux and Raspberry Pi and can be installed with the following command on Debian based distributions.

```
sudo apt-get install pcsxr
```

While there is an installer on Windows, the application is not actively supported and maintained in that environment, which means you may get lucky and the application will work. But otherwise on Windows, the recommendation is to use **Duck Station**.&#x20;

### ePSXe

Available On: Windows and Android

ePSXe is included on this list as it is probably one of the better known emulators out there, and the one I used the most growing up. Unfortunately ePSXe is closed source, which makes it hard to work with the save state format. But if someone knows what compression format is used, and where the memory and vram offsets are, it would make it similar to working with PCSXR or Duck Station.&#x20;

The main advantage that ePSXe could potentially have is the ability to run EXE files from Playstation outside of the CD image. This would make it possible to extract a CD image, run the EXE and then edit the files to debug what is where. Barring any of these approaches, ePSXe is most effective for simply playing and enjoying games.

### no$PSX

Available on: Windows

no$PSX is one of the most feature rich debugging environments for Playstation. The emulator lets you view the raw VRAM, has a memory viewer, and let's you stop and step through the game's instructions as they are executed. It is a very powerful tool that a brain-dead mouth breather like myself is not able to take full advantge of.&#x20;

### Duck Station

Available On: Windows and Android

Duck Station is one of the more recent emulators to come onto the scene, and also arguably the best. Duck Station has an extremely intuitive user interface, is semi-open source (for the Windows version at least), let's you toggle compression for the save states, let's you edit memory with a cheat interface and let's you also see the VRAM. While it's not quick the full package, it's very close to it.&#x20;

### RetroArch

Available on: Windows, Linux and Android

RetroArch is an emulation front end that allows you to install different emulation cores in order to be able to run different games across multiple systems from a unified user interface. For playstation two of these cores include PCSXR, and Duck Station.&#x20;

The only advantage I've found to working with RetroArch is that if you dig through the settings, there is an option to not use compression for save states. Otherwise RetroArch doesn't seem to offer any other debugging options. And in this respect RetroArch is less than the some of its parts. I find that it's better to use PCSXR or Duck Station directly and take advantage of using those programs directly as opposed to going through the extra step of using Retor Arch. This seems like program that is better for enjoying your retro games as opposed to digging into them.

## Memory Map

Arguably one of the largest advantages of working with the Playstation version is being able to take advantage of the limited amount of memory. The PlayStation has 2MB of main memory and 1MB of VRAM.&#x20;

What this means is that files are loaded into fixed locations in memory. This allows you to make a save state, and then search against the files to find out which ones are loaded into memory where. Once you find a file, you can edit it in the save state, reload the state and see how the game reacts to the changes.&#x20;

If you make too many changes and crash the game, you can always go back to a previous state. The main advantage of this approach is that it allows you to make changes and see how the game reacts if semi-real time. This allows you to narrow down and make very targeted changes in-game to figure out what specific bytes in a file are for.
