# Amstrad GX4000 / Plus Multi-Cartridge with up to 8 ROM slots

## Features

- Put up to 8 games on a single cartridge
- Selection via dip switches
- fits into standard cartridge shells
- noACID patch (does not require ACID/FPGA) based on Shinings design ()

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
| 1MBB | 27C080<br>27C801 | 8 | 4 | 2 |

Other EPROMs may work if they are fully compatible with those types. 

### Limitations



## PCB configuration

The PCB has been designed to be flexible and handle all kinds of combinations of game size and EPROM size. This requires that the assembly and soldering slightly differs, depending on the selected combination. 

### ROM size

First, check what the size of the games is that you want to store on a multi-cartridge. Make sure all games have the same size, e.g. 128K like the original GX4000 games had. 

It's not possible to mix different ROM sizes on the same EPROM. E.g. you can't select two 128K games and a 256K game and burn it onto the same EPROM to get a 3 games cartridge. <sup>If you are ever in such a situation, where it's not possible to have a collection of gaes with the same size you can fill up a 128K rom with 128K additional, empty space to bring it to 256K and then burn it together with another 256K game, as if both would be 256K.</sup>  

If you have selected game ROMs with 
- 128KB, then add the resistors for <b>A17,A18 and A19</b>
- 256KB, then add the resistors for <b>A18 and A19</b> and close the link for 256K ROMs (LK4).
- 512KB, then add the resistors for <b>A19</b> and close the links for 512K ROMs (LK2 <b>and</b> LK4).

<img src="/pictures/multicart_LKbridges.jpg" width="1200"/>

