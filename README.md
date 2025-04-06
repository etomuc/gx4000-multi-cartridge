# Amstrad GX4000 / Plus Multi-Cartridge with up to 8 ROM slots

## Features

- Put up to 8 games on a single cartridge
- Selection via dip switches
- same PCB size as original cartridges
- https://www.cpcwiki.eu/forum/amstrad-cpc-hardware/amstrad-gx4000-plus-cartridge-pcb/msg210695/#msg210695
- no ACID required (implements noACID patch based on [Shinings design]([https://www.cpcwiki.eu/forum/amstrad-cpc-hardware/amstrad-gx4000-plus-cartridge-pcb/msg210695/#msg210695]) )

- [Shining]([url](https://www.cpcwiki.eu/forum/amstrad-cpc-hardware/amstrad-gx4000-plus-cartridge-pcb/msg210695/#msg210695))

## Multi-cartridges

An GX4000 / Amstrad Plus cartridge typically[^1] holds a ROM/EPROM with 128KB, 256KB or 512KB of data. E.g. all original GX4000 games were using 128K ROMs while more recent released can hold up to 512K, like "La Culotte de Zelda".
Multi-Cartridges have been available for many years now, the most famous probably being the 32-in-1 which holds all original, commercial releases for the GX4000. A multi-cartridge usually holds one or more EPROMs that can store more than a single game and offers to select between the games via switches. While the 32-in-1 is a nice thing, it's biggest downside is, that it is much bigger than an original cartridge and doesn't even fit into a Plus. 

The cartridge here resembles the dimensions of the original cartridge PCB and fits into a standard cartridge case. It can hold up to 8 games, depending on the selected games and EPROMs. 

[^1]: It also supports ROMs with 32 or 64KB, but this is rarely used and not implemented on this cartridge. For cartridge details see here: https://www.cpcwiki.eu/index.php/GX4000_cartridge

### Supported Eproms

This cartridge here supports a wide variety of EPROMS with 128KB, 256KB, 512KB and 1024KB of total capacity. If your EPROM is bigger than a single ROM that you want to burn to the EPROM you have the possibility to leverage the remaining space for additional games.

Examples of EPROMs and how many games they can hold: 

| Size | Name | 128K games | 256K games | 512K games |
| --- | --- | --- | --- | --- |
| 128KB | 27C010<br>27C1001<br>27C1000 | 1 | / | / |
| 256KB | 27C020<br>27C2001<br>27C2000 | 2 | 1 | / |
| 512KB | 27C040<br>27C4001<br>27C4000 | 4 | 2 | 1 |
| 1MB | 27C080<br>27C801 | 8 | 4 | 2 |

Other EPROMs may work if they are fully compatible with those types. 


## PCB configuration

The PCB has been designed to be flexible and handle all kinds of combinations of game size and EPROM size. This requires that the assembly and soldering slightly differs, depending on the selected combination. 

### ROM size - LK links 2,4 and resistors 1-3

First, check what the size of the games is that you want to store on a multi-cartridge. Make sure all games have the same size, e.g. 128K like the original GX4000 games had. 

It's not possible to mix different ROM sizes on the same EPROM. E.g. you can't select two 128K games and a 256K game and burn it onto the same EPROM to get a 3 games cartridge. <sup>If you are ever in such a situation, where it's not possible to have a collection of gaes with the same size you can fill up a 128K rom with 128K additional, empty space to bring it to 256K and then burn it together with another 256K game, as if both would be 256K.</sup>  

If you have selected game ROMs with 
- 128KB, then add the resistors <b>1,2 and 3</b>. Don't close any link.
- 256KB, then add the resistors <b>2 and 3</b> and close the link for 256K ROMs (LK4).
- 512KB, then add only the resistor <b>3</b> and close both links for 512K ROMs (LK2 <b>and</b> LK4).

<img src="/pictures/multicart_LKbridges.jpg" width="1200"/>

### Game selector - dip switches

Which DIP switches need to be populated depends on the size of your game ROMs and the size of your EPROM.

You need a DIP switch where both criteria are fulfilled: 
- your EPROM is at least the size indicated on the PCB below the DIP switch
- below that DIP switch is a resistor

<img src="/pictures/multicart_pcbconfig.jpg" width="1200"/>

## ROM configuration

GX4000 cartridge ROMs are usually provided as a .CPR file. To burn such a cartridge file to an EPROM the CPR first has to be converted into a pure binary ROM image. You can use CPRTools for this task: http://www.cpcmania.com/cprtools/cprtools.htm

If you are burning only a single game to your EPROM you are already set after the conversion. 

If you want to burn more than a single game to the EPROM make sure to convert all CPRs to ROM files. After that you need to combine all ROMs into a single, large ROM. This can be done with various tools. On Windows you can e.g. use the COPY command in command prompt. 

Example: 
Let's assume you want to burn 4 games with 128K each into a single 27C040 EPROM. The game ROMs have the names copter.rom, kickbox.rom, pinball.rom and switch.rom. Make sure all .rom files are in the same folder. Open command prompt in this folder and enter: 

<code>copy /b copter.rom+kickbox.rom+pinball.rom+switch.rom 4gamesin1.rom</code>


This will give you a file "4gamesin1.rom" with a size of exactly 512KB (524,800 Bytes) that you can burn to your 27C040 EPROM.
