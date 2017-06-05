# Contributing
Contributions to the Citra Games Wiki are welcomed, as keeping all of the data up to date and accurate is a community effort. There are 2 parts to the Wiki:
 - [Code](#code)
 - [Wiki](#wiki)

Throughout this guide, code blocks like `<Value>` are used. This means that "Value" should be replaced by something, and the "<>" should be deleted.

In this repo, DAT files follow the TOML syntax, where each line consists of `<key> = <value>`. Value can either be a string (Words with surrounding quotes.), an integer (Number with no quotes.), or a boolean (`true` or `false`.). There can also be an array of tables in a DAT file (A group of values.), which look like `[[ <name> ]]`.

All dates follow the format `<4-Digit Year>-<2-Digit Month>-<2-Digit Day>`. For example, June 3rd 2017 would be "2017-06-03".

Title IDs can be found near the top of a log when running a game. For example, this is what it looks like for The Legend of Zelda: Ocarina of Time: `[   0.019882] Loader <Info> core/loader/ncch.cpp:Load:340: Program ID: 0004000000033500`.

## Code
The code consists of the actual files in the Github repisitory. To modify them, you have to fork this repo, make your changes, and send a pull request.

At the root, there's a folder for each game. The names of these folders should follow these specifications:
- Only use letters, numbers, and hyphens (No spaces!), because they will be linked to on the site.
- Use proper capitalization, for consistency.
- Have a wiki page with the same name.

### Metadata
The metadata for the game is located at `/<Game Name>/game.dat`. This is required info about the game. The DAT values are:
- `title` (String): English title of the game. This doesn't have to match the wiki or foldeer name, so there can be spaces.
- `description` (String): Short, 1-2 line description of the game. Get these from [Wikipedia](https://en.wikipedia.org/wiki/List_of_Nintendo_3DS_games).
- `compatibility` (Integer): How well the game works in Citra. A reference can be found [here](https://citra-emu.org/game/), with `Won't Boot` being `0`, and `Perfect` being `5`.
- `tested_date` (String): Last date the game was tested on.
- `tested_version` (String): Last version of Citra the game was tested on.
- `needs_system_files` (Boolean): Whether the game requests the system files or not, regardless of whether it could be played without them.
- `needs_shared_font` (Boolean): Whether the game requests the shared font or not, regardless of whether it could be played without them.
- `tested_by` (String): Your forum account name, if you have one. If you don't, don't include this line.

- `releases` (Array of tables): Info about each release of the game.
  - `title` (String): Title ID of this release of the game.
  - `region` (String): Region of the game. Possible values are:
    - `AUS`
    - `CHN`
    - `EUR`
    - `JPN`
    - `KOR`
    - `TWN`
    - `USA`
  - `release_date` (String): When the game was released in this region.

An example of a game metadata file is the one for [The Legend of Zelda: Ocarina of Time](https://github.com/citra-emu/citra-games-wiki/blob/master/Legend-of-Zelda-Ocarina-of-Time/game.dat):
```js
title = "The Legend of Zelda: Ocarina of Time 3D"
description = "The Legend of Zelda: Ocarina of Time 3D is an action-adventure video game co-developed by Grezzo and Nintendo EAD Tokyo and published by Nintendo for the Nintendo 3DS handheld game console. The game was released worldwide in June 2011."
compatibility = 5
tested_date = "2017-06-03"
tested_version = "HEAD-a7ddec8"
needs_system_files = false
needs_shared_font = false
tested_by = "Flamboyant_Ham"

[[ releases ]]
title = "0004000000033500"
region = "USA"
release_date = "2011-06-19"
```

### Icon
The icon for a game is located at `/<Game Name>/boxart.png`. The suggested process for getting one is:
- Make sure the ROM for the game is in your Citra game directory.
- Take a screenshot of Citra's library listing.
- Crop out the game icon.

Game icons should not be compressed.

### Boxart
The boxart for the game is located at `/<Game Name>/boxart.png`. The suggested process for getting one is:
- Download a scan from [GameTDB](http://www.gametdb.com/), preferably with the `Nintendo 3DS` logo on the right.
- Downsize it to approximately `328x300` using [PicResize](http://www.picresize.com/).
- Compress it using [TinyPNG](https://tinypng.com/).

### Screenshots
The screenshots for the game are located in `/<Game Name>/screenshots/`. Screenshots **must** follow these specifications:
  - Native resolution.
  - Smallest window size.
  - Black background (For the blank space left and right of the bottom screen.). To achieve this, go to the [User Directory](https://citra-emu.org/wiki/user-directory/), and from there navigate to the `config` directory. Open qt-config.ini with a text editor, and set bg_blue, bg_green, and bg_red to 0.
  - Not compressed.

The name of the screenshot doesn't matter.

### Savefiles
#### Metadata
The metadata for a save is located at `/<Game Name>/savefiles/<Save Name>.dat`. This is info about the save. The DAT values are:
- `title` (String): The location of the save ingame.
- `description` (String): A brief explanation about the save.
- `author` (String): Your forum account name, if you have one. If you don't, don't include this line.
- `title_id` (String): Title ID of the game.

#### Save Data
The save data is located at `/<Game Name>/savefiles/<Save Name>.zip`. To make a ZIP file, the process is:
- Make sure the ROM for the game is in your Citra game directory.
- Right click on the game and click `Open Save Data Location`. This should open a folder named `data`.
- Note the folder that the `data` folder is in. This is the low Title ID. As an example, the low Title ID for The Legend of Zelda: Ocarina of Time is `00033500`.
- The folder that the low Title ID folder is in should be named `00040000`, the high Title ID.
- Copy the high title ID folder elsewhere.
- Delete everything from the high title ID folder except for the low Title ID folder.
- Compress the high title ID folder into a ZIP.

## Wiki
The wiki contains info about specific game problems, and can be modified by anyone. They use [Markdown](https://guides.github.com/features/mastering-markdown/) formatting.

Each page's title should match the game's respective folder in the code section, except with hyphens in the code changed to spaces on the wiki.

The format of each page is as follows:
- H2 header with text saying `Summary`.
- Brief summary of how the game performs.
- H3 subheader saying `Problems`.
- For each problem, a bullet describing an issue the game has.
- For each of those bullets, make a sub-bullet linking to the relevant Github issue on `citra-emu`.
- If there's any relevant media, make another sub-bullet linking to it.

An example of a game wiki page is the one for [Mario Kart 7](https://github.com/citra-emu/citra-games-wiki/wiki/Mario-Kart-7):
```markdown
## Summary
Mario Kart 7 has some problems in Citra. It is playable, but there are minor graphical glitches.

### Problems
- Random crashes may occur.
  - Github Issue: [#2443](https://github.com/citra-emu/citra/issues/2443).
- All particle effects (Such as smoke, tire tracks, or drift sparks.) are rendered incorrectly. They may copy HUD elements, or just be black.
  - Github Issue: [#1887](https://github.com/citra-emu/citra/issues/1887).
- Looping audio buffers aren't supported.
  - Github Issue: [#2093](https://github.com/citra-emu/citra/issues/2093).
- When using the software renderer, Mii characters are not rendered.
  - Github Issue: [#1749](https://github.com/citra-emu/citra/issues/1749)
```
