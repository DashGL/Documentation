# DAT (PC)

`.DAT` is the file extension used for the PC versions bundle format. The term "bundle" is used in favor of "archive" as the purpose of these files isn't to compress the contents as all of the files are in a non-compressed state in the file. The purpose of these files is to group the assets needed for scene files into specific files.&#x20;

What this means is if the game wants to load in all of the assets needed for stage 0x0f, scene 0x00. The game will load the file `ST0F.DAT` to load the map data, and then `ST0F00.DAT` for all of the NPC's and enemies that make up that scenario. If the game changes scenes to stage 0x0f, scene 0x01, the game will load `ST0F01.DAT` for the NPC's and enemies for that scenario.&#x20;

This means that multiple copies of the same asset can be copied into the different scenarios they are used in. Also note that the game will used `ST0F00.DAT` for assets such as 3d models associated with that scene, and `ST0F00T.DAT` for textures used in that scene.&#x20;
