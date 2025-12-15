# Multi-Cartridge with up to 8 ROM slots<br>for Amstrad GX4000 / Amstrad Plus 

An GX4000 / Amstrad Plus cartridge typically[^2] holds a ROM/EPROM with 128KB, 256KB or 512KB of data. E.g. all original GX4000 games were using 128K ROMs but more recent released games often need more storage and can hold up to 512K, like e.g. "La Culotte de Zelda".

[^2]: It also supports ROMs with 32 or 64KB, but this is rarely used and not implemented on this cartridge. For cartridge details see here: https://www.cpcwiki.eu/index.php/GX4000_cartridge

Multi-Cartridges have been available for many years now, the most famous probably being the 32-in-1 which holds all original, commercial releases for the GX4000. A multi-cartridge usually carries one or more EPROMs where each EPROM can store more than a single game. The games can be selected via DIP switches. While the 32-in-1 is a nice thing, it's biggest downside is, that it is much bigger than an original cartridge and doesn't even fit into a Amstrad Plus computers. 

The cartridge here resembles the dimensions of the original cartridge PCB and fits into a standard cartridge case. It can hold up to 8 games on a single EPROM (depending on the selected games and EPROM types). 

<img src="/pictures/pcb.jpg" width="300"/>

> [!TIP]
> Although this documentation talks about game ROMs you can of course also put applications and OS in each of the ROM slots. This way you can e.g. create your personal boot-cartridge for all language variations or with/without Parados, or with/without Burniung Rubber ,or with SymbOS as an alternative OS, or Firmware 3.x , or ... 

## Features

- Put up to 8 games on a single cartridge
- Selection via dip switches
- same PCB size as original cartridges
- no ACID required (implements noACID patch based on [Shinings design](https://www.cpcwiki.eu/forum/amstrad-cpc-hardware/amstrad-gx4000-plus-cartridge-pcb/msg210695/#msg210695))

## License

The project is released under the CC BY-NC-ND 4.0 license with the following enhancements: The cartridge and all resources are free to use for personal use. 
Selling a cartridge based on this PCB in any form commercially is strongly forbidden. The only exception are homebrew productions if the copyright holders of the 
software included on the cartridge have given their official permission for a commercial production. 

In other words: don't use this PCB if you want to make money with bootleg and piracy cartridges. 

### Disclaimer

> [!CAUTION]
>**USE AT YOUR OWN RISK.**
>
>This is a hobby project, I am a hobbyist and no engineer. There is always the risk that the cartridge can cause harm to your computer/console. 
>Although I have tested the cartrdidge on my Plus and GX4000 with many different EPROMS, there is no guarantee that it will properly work under all circumstances.
>
> Especially if you are building this for others (commercially or not) make sure to make your own intense tests to guarentee this cartridge works as expected before handing over to the recipients.  
>
>**USE AT YOUR OWN RISK.** 


## Building a cartridge

For a full assembly you need 
- basic soldering skills - as long as you can solder normal through hole components reliably, you will be fine.
- an option to program EPROMs
- optionally (but recommended): a 3D printer to print the cartridge cases

### Bill of Materials

| Part | Quantity |
| --- | --- |
| PCB | 1 |
| IC EPROM 128K - 1MB<br><sup>See "PCB configuration" below  | 1 |
| IC 74AC112 or 74F112<br><sup>maybe also 74HC(T)112[^1]</sup>| 1 |
| Dip-Switch (1,2 or 3 switches)<br><sup>See "Supported Eproms" below | 1 <br><sup>(or 0)</sup> |
| Capacitor 100nF 104 5mm | 2 |
| Capacitor <b>100pF</b> 101 5mm | 1 |
| Resistor 4.7k 1/4W | 2 - 5 |

[^1]: AC(T) or F is recommended as they are faster than HC(T) types, however several users have reported that 74HC(T)112 perfectly work

It's possible to use a socket for the EPROM however it will no longer fit into a cartridge shell. 

### PCB

You can order PCBs easily here: https://www.pcbway.com/project/shareproject/Amstrad_GX4000_Multi_ROM_cartridge_9637c211.html

Note: For easier insertion select 30° beveling for the edge connector. 

### Assembly

Note: Using sockets is possible but if you want to put the cartridge into a 3D printed shell you need to solder the ICs directly to the PCB without sockets.

1) program the EPROM <sup>(see "Rom configuration" below)</sup>
2) solder the EPROM and the 74xx112 IC directly to the PCB
3) continue with the required resistors and close the respective LK joints <sup>check the "PCB configuration" section below </sup>
4) add all capacitors. Pay attention that one capacitor is 100pF, two are 100nF.
5) finally add the DIP switch

A 3D printable case shell can be found in the "files" folder. 

### Supported Eproms

This cartridge here supports a wide variety of EPROMS with 128KB, 256KB, 512KB and 1024KB of total capacity. If your EPROM is bigger than a single ROM that you want to burn to the EPROM you have the possibility to leverage the remaining space for additional games.

Examples of EPROMs and how many games they can hold: 

| Size | Name | 128K games | 256K games | 512K games |
| --- | --- | --- | --- | --- |
| 128KB | 27C010<br>27C1001<br>27C1000 | 1 | - | - |
| 256KB | 27C020<br>27C2001<br>27C2000 | 2 | 1 | - |
| 512KB | 27C040<br>27C4001<br>27C4000 | 4 | 2 | 1 |
| 1MB | 27C080<br>27C801 | 8 | 4 | 2 |

Other EPROMs may work if they are fully compatible with those types. 

The 29F040 EEPROM can be used with slight modifications (see below).

## PCB configuration

The PCB has been designed to be flexible and handle all kinds of combinations of game size and EPROM size. This requires that the assembly and soldering slightly differs, depending on the selected combination. 

### LK links 2,4 and resistors 1-3 (ROM size)

First, check what the size of the games is that you want to store on a multi-cartridge. Make sure all games have the same size, e.g. 128K like the original GX4000 games had. 

It's not possible to mix different ROM sizes on the same EPROM[^3]. E.g. you can't select two 128K games and a 256K game and burn it onto the same EPROM to get a 3 games cartridge.
[^3]:If you are ever in such a situation, where it's not possible to have a collection of gaes with the same size you can fill up a 128K rom with 128K additional, empty space to bring it to 256K and then burn it together with another 256K game, as if both would be 256K.

If you have selected game ROMs with 
- 128KB, then add the resistors <b>1,2 and 3</b>. Don't close any link.
- 256KB, then add the resistors <b>2 and 3</b> and close the link for 256K ROMs (LK4[^4]).
- 512KB, then add only the resistor <b>3</b> and close both links for 512K ROMs (LK2 <b>and</b> LK4[^4]).

[^4]: Why 2 and 4 but there is no 1 or 3? They have been named according to the LK IDs on the original cartridge PCB. 

### Dip switches (ROM/Game selection)

Which DIP switches need to be populated depends on the size of your game ROMs and the size of your EPROM.

You need a DIP switch where both criteria are fulfilled: 
- your EPROM is at least the size indicated on the PCB below the DIP switch
- below that DIP switch is a resistor

<b>See all possible combinations of LK bridges, resistors and DIP switches here:</b>

<img src="/pictures/multicart_pcbconfig.jpg" width="1200"/>

- Red bars are solder bridges. Close these bridges with solder and/or wire to ensure proper functionality.
- You can also burn a single ROM into a larger EPROM, e.g. a 128K game into a 512K EPROM. For those cases just chose the config as if the EPROM would have the right size (e.g. 128K/128K or 512K/512K).

## Combine game ROMs to burn a single binary into an EPROM

GX4000 cartridge ROMs are usually provided as a .CPR file. To burn such a cartridge file to an EPROM the CPR first has to be converted into a pure binary ROM image. You can use CPRTools for this task: http://www.cpcmania.com/cprtools/cprtools.htm

If you are burning only a single game to your EPROM you are already set after the conversion. 

If you want to burn more than a single game to the EPROM make sure to convert all CPRs to ROM files. After that you need to combine all ROMs into a single, large ROM. This can be done with various tools. On Windows you can e.g. use the COPY command in command prompt. 

Example: 
Let's assume you want to burn 4 games with 128K each into a single 27C040 EPROM. The game ROMs have the names copter.rom, kickbox.rom, pinball.rom and switch.rom. Make sure all .rom files are in the same folder. Open command prompt in this folder and enter: 

<code>copy /b copter.rom+kickbox.rom+pinball.rom+switch.rom 4gamesin1.rom</code>

This will give you a file "4gamesin1.rom" with a size of exactly 512KB (524,800 Bytes) that you can burn to your 27C040 EPROM.

> [!IMPORTANT]
> All your source ROMs must have exactly 128K, 256K or 512K and the resulting file must be exactly 256K, 512K or 1MB. Even the slightest deviation will most likely result in corrupt EPROM content.

## Game selection

If everything works well, you can now start your GX4000 with an 8-in-1 games cartridge. 

You can select which game to play using the DIP switches on top of the cartridge. 

<img src="/pictures/selectromposition.jpg" width="1200"/>

> [!IMPORTANT]
> NEVER switch games/roms while your GX4000/Plus is turned on. Always turn off before switching to another position. 

### Using a 29F040 EEPROM 

> [!CAUTION]
>This mod is based on the data sheet and has not been verified yet. Please verify its correctness before using the cartridge in a computer/console. 

The 29F040 EEPROM has a slightly different pin layout but you can use this EEPROM similar to a 512K EPROM with these slight modifications: 

<b>On the bottom of the PCB:</b>

1) Cut one trace at the indicated location:
<img src="/pictures/29F040bottom.jpg" height="300px"/>
   
<b>On the top of the PCB:</b>

2) Don't add resistor 3 at it's normal position but below as indicated.
3) Make a junction between resistor 2 and 3 as indicated.

<img src="/pictures/29F040top.jpg" height="300px"/>
