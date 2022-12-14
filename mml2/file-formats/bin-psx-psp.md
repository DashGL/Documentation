# BIN (PSX/PSP)

`.BIN` is the file extension used for the PSX versions bundle format. The term "bundle" is used in favor of "archive" as the purpose of these files isn't to compress the contents, though notably the textures and map files are compressed. The reason for this seems to be for getting around space limitations of the PSX game disk. The `.BIN` format itself contains a lot of padding and is not a space effecient storage format. The reason for this spacing is likely to align with tracks on the disk in order to optimize copying assets into memory.&#x20;

The purpose of `.BIN` files is to group the assets needed for scene files into specific files. What this means is if the game wants to load in all of the assets needed for stage 0x0f, scene 0x00. The game will load the file `ST0F.BIN` to load the map data, and then `ST0F00.BIN` for all of the NPC's and enemies that make up that scenario. If the game changes scenes to stage 0x0f, scene 0x01, the game will load `ST0F01.BIN` for the NPC's and enemies for that scenario.&#x20;

Multiple copies of the same asset can be copied into the different scenarios they are used in. Though in the case of Megaman Legends 2 the linear game design means that each Stage does not have very many scenes. And the same assets are not often used between stages. Also note that the game will used `ST0F00.BIN` for assets such as 3d models associated with that scene, and `ST0F00T.BIN` for textures used in that scene.&#x20;

## Structure

* Files are declared as offsets of 0x400
* First `uint32_t` is the type
* File extensions are not included, like in Megaman Legends 1
* Second `uint32_t` is the length
  * in the case of compressed files, this is the length of the full uncompressed data
* The fourth `uint32_t` is the position in memory where the file is copied into (if included)
