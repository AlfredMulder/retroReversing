---
layout: post
tags: 
- ps1
- reverseengineering
title: Playstation 1 Games with Debug Symbols
thumbnail: /public/consoles/Sony Playstation.png
image: /public/consoles/Sony Playstation.png
permalink: /ps1-debug-symbols
breadcrumbs:
  - name: Home
    url: /
  - name: Sony Playstation 1
    url: /ps1
  - name: Playstation 1 Games with Debug Symbols
    url: #
recommend: ps1
editlink: /ps1/PS1Symbols.md
---

I have never seen a PS1 executable bigger than 2mb, normally if they require more code they split it into multiple executables. 
With memory being so precious it would be unlikely a developer would forget to strip the debug symbols from an executable. 
However it is possible to find symbols included on the disk in various formats, one of those formats is SYM:
* CyberTiger has GOLF.SYM
* BrunswickCircuitProBowling has THQB2.SYM
* Chill (Europe) seems to have lots of source code in it! incide CDFILLER, includes C files!! Might just be the names of the files tho…
* Digimon World contains quite a lot of what look like symbols in MOV_REL.BIN
* Disneys 101 Dalmarions Patches London contains MAIN.SYM also MAIN.MAP!!! that can be used to put symbols back in game
* DivideThe EnemiesWithin contains GAME.SYM and looks like it uses C++!
* DoraTheExplorer has MAIN.SYM
* Frogger2 seems to contain Makefiles
* JackieChanStuntmaster contains GAME_REL.SYM!!!
* KnockoutKings contains MAIN.MAP with address name mapping

# Linker Map file Format
The .MAP file created by a c/c++ linker such as LD follows the format:
```
Start     Stop   Length      Obj Group            Section name
80010000 800179C3 000079C4 80010000 text             .rdata
...
Program entry point : 00000000
Address  Names alphabetically
8008CEF4  CD_ready
```
These files contain all the information you need to get the full debug symbols back for a game! You just need to parse them and add them to your dissassembler of choice (e.g Radare2 or IDA Pro)

# Games with FULL Linker Map file

Game Name | Map File
--- | --- 
Brunswick Circuit Pro Bowling 2 | THQB2R.MAP
Disney's 101 Dalmatians 2 | /DATA/MAIN.MAP
Dora the Explorer - Barnyard Buddies | /DATA/MAIN.MAP
Knockout Kings | /DATA/MAIN.MAP
---

These ones crashed while getting contents:
* CastrolHondaSuperbikeRacing - BIKE.SYM

Other Interesting:
* Disney GoofysFunHouse contains string - "dbugpsx /h /epsx.cpe /m-  psx.sym"