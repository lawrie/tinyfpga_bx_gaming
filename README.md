# TinyFPGA BX Gaming

This repository documents how to use the TinyFPGA BX as a Games Console.

This project was started by a [Discussion](https://discourse.tinyfpga.com/t/bx-portable-game-console-project-collaboration/553) on the TinyFPGA forum.

## Overview

A Field Programmable Gate Array (FPGA) is capable of emulating hardware such as an audio synthesizer, a Graphics Processing Unit (GPU), 
and drivers for devices such as a VGA screen or an Liquid Cyystal Display (LCD), game controllers, buttons, etc. It is also capable of implementing a CPU as a Soft Processor.

This means that an FPGA such as the TinyFPGA BX can replace all the chips used in early games consoles and home computers.

The approach taken here is to to use the [picorv32](https://github.com/cliffordwolf/picorv32) implementation of [Risc-V](https://en.wikipedia.org/wiki/RISC-V) for the CPU 
that runs the games. However, it is also possible to use other soft processors, such as a 6502 CPU or a Z80 CPU for specific games.

The TinyFPGA has the resources to emulate games consoles, arcade machines and home computers of the late 1970s, and early 1980s. With extra RAM it could emulate more early
80s home computers. The myStorm BlackIce II board which uses a similar (but faster) FPGA has 256kb of external SRAM, which enables it to emulate home computers, such as
the Acorn Atom and the BBC Micro.

The next generation of open source FPGAs based on the ECP5 FPGA will be needed for computers and consoles of the late 80s and early 90s, such as the Commodore Amiga.

I will concentate on a portable Games Console that drives a 320 by 240 LCD, but the code in the repositories referenced also supports TV games consoles driven by VGA.
Future implementations based on the ECP5 will support HDMI.

The hardware that I am using for the portable Games console was produced by [Fabien Chouteau](https://github.com/Fabien-Chouteau/field-programmable-game-console).

![Games Console](https://discourse.tinyfpga.com/uploads/default/optimized/1X/f4435f46beb1bc25ac96b8b072648f0aa48cb1bf_1_690x388.jpeg "Games Console")

![Games Console back](https://discourse.tinyfpga.com/uploads/default/optimized/1X/fbad9ec2068b6b4feefcab10d31f3769fc382d1a_1_690x388.jpeg "Games Console back")

The TinyFPGA BX has 16kb of BRAM, or which 2kb is used by picorv32. This allows a RAM-only version of [PicoSoC](https://github.com/cliffordwolf/picorv32/tree/master/picosoc) 
to be used that has 14kb of RAM for the code, data and video RAM. This is sufficient for emulating early consoles such as the Atari 2600.

The TinyFPGA also has 1 Mb of flash memory. A significant fraction is available for executing code from. So a version of PicoSoC can be produced that runs the code 
from flash memory allowing much bigger programs, but still limiting VGA buffers and writeable data to 14kb.

### LCD Screen

The [LCD Screen](https://www.buydisplay.com/default/2-8-inch-tft-touch-shield-for-arduino-w-capacitive-touch-screen-module) used is a 320 x 240 screen
using the 8-bit 8080 driver and without any touchscreen option.

### Audio

The audio is based on Dave Gundy's [tiny-synth](https://github.com/gundy/tiny-synth) project which implements an audio synthesizer similar to the 
[Commodore C64 SID](https://www.c64-wiki.com/wiki/SID) chip.

## Early History of Video Gaming

### Arcade machine games

The earliest video games were implemented using dedicated hardware in arcade machines. Two of the earliest successful ones were Pong and Space Invaders.

![Arcade Game](https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Video_game_-_Ms_Pacman_and_Galaga.jpg/1280px-Video_game_-_Ms_Pacman_and_Galaga.jpg "Arcade Game")

#### Pong

As well as  arcade machine dedicated games machines that plugged into a home TV were produced, such as the 
[Atari Pong machine](https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/TeleGames-Atari-Pong.png/330px-TeleGames-Atari-Pong.png).

Pong is such a simple game that it can be implemented on an FPGA without using a CPU. [Here](https://github.com/lawrie/tinyfpga_examples/tree/master/pong) is my port of the 
Pong game from the [fpga4fun site](https://www.fpga4fun.com/PongGame.html), running on the Tiny FPGA BX. It uses a rotary encoder to control the board and uses VGA output. 
It is not the full pong games as it only has one player, and does not show the score, but could easily be modified to be more like the original pong game.

![Fpga4fun Pong](https://discourse.tinyfpga.com/uploads/default/original/1X/e4ccbf25da97bfff96cda172fdfdac4a033995c4.jpg "Fpga4fun Pong")

#### Space Invaders

Slightly more sophisticated games such as Space Invaders could be implemented without a CPU, but it is hard to do that, and much easier using a CPU.

I ported the FPGAWars group's start of a [Space Invaders game](https://github.com/lawrie/Space-Invaders) to the TinyFPGA BX.

#### Asteroids

Another successful arcade game was asteroids. The arcade game used vector graphics to generate the video signal.

We are porting Asteroids to the handheld games console - see below.

#### Pacman

The first really successful Arcade Game surpassing Pong and Space Invaders by some distance, was PacMan.

We have a version of PacMan running on the [tiny_fpga_bx_game_soc](https://github.com/lawrie/tinyfpga-bx-game-soc/tree/develop/games/pacman_lcd). 
It can use a VGA monitor or can run on our handheld console. Our version is closer to the layout used on the Nintendo Entertainment System game console (see below)
than the arcade game version.

#### Other arcade games

Other very successful Arcade games included Defender, Donkey Kong, Frogger, Galaga, Joust and Ms PacMan. Ports of some of these to our games console may ber coming.

### Home Games Consoles

#### Atari 2600

The first really successful games console was the Atari 2600. It used a chip called the Television Interface Adapter (TIA) to generate TV output on the fly.

There were ports of arcade games such as Pong, Space Invaders for the Atari 2600, but soon new games were being produced by Atari for the 2600.

##### Adventure

One example is Adventure by Warren Robinett:

![Easter Egg](https://upload.wikimedia.org/wikipedia/en/7/73/Adventure_Easteregg.PNG "Easter Egg")

[Adventure and its Easter Egg](https://www.youtube.com/watch?v=VYmfEx3taAM&t=363) are a prominent part of the plot of Steven Spielberg's Ready Player One.

##### Pitfall

Games developers did not get recognition or royalties for their games at Atari, so several of their programmers left to form Activision. One of their most successful games 
for the Atari 2600 was Pitfall.

After the Video game crash of 1983, leadership in games console market moved from North America to Japan. The Nintendo Entertainment System (NES) was the most successful.

#### Nintendo NES

The game that led sales of the NES was Super Mario Bros, developing the characters of Mario and his brother Luigi, who had been introduced in the earlier
aracde games Donkey Kong and Mario Bros.

##### Super Mario Bros

We have the start of a port of Super Mario Bros to our games console.

#### Nintendo SNES

After a few years the 8-bit NES was replaced by the 16-bit Super NES. The Super NES supported multiple video modes the most interesting of which
was mode 7 which implemented a simple 3D view. 

##### Mario Kart

A successful game that used mode 7 was Super Mario Kart.

There is a demo of using the TinyFPGA to do something like mode7:

<<<<<<< HEAD
![Mode7](https://img.youtube.com/vi/vtXhnkemzLw/0.jpg "Mode7")

[Mode 7] (https://youtu.be/vtXhnkemzLw "Mode7")
=======
![Mode7](https://www.youtube.com/embed/vtXhnkemzLw)

[Mode 7](https://youtu.be/vtXhnkemzLw "Mode7")
>>>>>>> f2e2c260f25fefbcf132ab2d2e4faae95f49c567


### Handheld games consoles

The most succesful early handheld games console was the Nintendo Gameboy. The original was black and white but that a colour version, the Gameboy Color 
followed soon, and later the Gameboy Advance. Our games console has a similar form-factor to the Gameboy Advance, but later version of the Advance movedto a clamshell design.

#### Nintendo Gameboy

##### Tetris

The game that was launched with the Gameboy and ensured its success was Tetris.

We have a port of Tetris on our games console.

### Home Computers

There are some early home computers that were important in the history of gaming.

#### Apple One

The Apple One was not such a machine as only a tiny number were produced, but it is interesting for the way that it generated its video signal.
There is a port of the Apple One to several icestorm FPGAs including the TinyFPGA B2 and the mystorm BlackIce II.

The game Breakout was produced by Steve Wozniak, the designer of the Apple One and the Apple Two. He produced it for the Atari 2600.

#### Sinclair ZX Spectrum

The ZX Spectrum was a very cheap home computer that very many games were produced for.

#### Acorn Atom and BBC Micro

Other UK home computers were the Acorn Atom and its much more powerful successor, the BBC Micro. There arte ports for these for the mystorm BlackIce II.

#### Commodore C64

The Commodore C64 was the most succesful home compter ever produced, and was designed for games. Many successful games were produced for it.

The video system for our games console takes several ideas from the C64 video system and bases its audio system or the C64 SID chip.

#### Commodore Amiga

The Amiga is too complex to implement on the TintFPGA BX, but [here it is](https://www.youtube.com/watch?v=q0nysMydf4I) running on a Lattice ECP5 open source board,
for which the icestorm toolchain is nearly ready, so this might be feasible on the next round of open source FPGA, possibly on the TinyFPGA EX.

## Graphics Processing Units

What are now called Graphics Processing Units started life as very simple devices to support writing to TV screens using minimals resource such as RAM and CPU time.

### Apple One

The Apple One computer had an extremely simple chip for driving the TV. There is an implementation of the Apple One on the TinyFPGA BX.

### Atari TIA

Another early example is the Television Interface Adapter (TIA) used by the Atari 2600.

### NES Picture Processing Unit (PPU)

### SNES modes

## Building your own version

### The hardware

You will need a TinyFPGA BX, which can be bought from a variety of sources including [Tindie](https://www.tindie.com/products/tinyfpga/tinyfpga-bx/), 
[Sparkfun](https://www.sparkfun.com/products/14829) and [Amazon UK](https://www.amazon.co.uk/TinyFPGA-BX-Without-Pins/dp/B07HCXTNFX/ref=sr_1_1).

To build the portable version you will need to get a version of Fabien Chouseau's PCB or build your own.

There are not many components on the PCB. There are the headers for the TintFPGA and the LCD screen, connectors for the batteries,
a switch and an audio connector. There are also 7 SMD passive devices: 4 capacitors, 2 resistors and a diode.

You will also need the LCD screen.

### Unix machine or VM

You will need a Unix machine to build the software. This can be a MAC or a Linux box, or a VM on a Windows machine. 

You should install the TinyFPGA tools and the picov32 GNU compiler.

### Games

There are a variety of games that you can build for the console, or you can write your own.

Games that use the RAM SoC consist of just a hardware.bin file containing the FPGA configuration bitstream. This file is always 135100 bytes long.

Games that use the SPI flash memory version of PicoSoC have a firmware.bin file as well that contains code and read-only data. Executing code from
SPI flash memory is slower than executing it from RAM, particularly when jumpos are done, interrupting the serial reading of the flash data.

A firmware.bin file can be of any length.

The hardware.bin file can be concatentated with the firmware.bin file with padding in betweewn to form a single file for the SD card menu - see below.

#### Dave Gundy's demo

#### Pacman

![Pacman](https://discourse.tinyfpga.com/uploads/default/original/1X/5a128efae7be41d5a157ea954480067cdb7e602e.jpeg "Pacman")

#### Tetris 

#### Super Mario Bros

#### Asteroids

![Asteroids](https://discourse.tinyfpga.com/uploads/default/optimized/1X/99cb87082d2940259fdba1fb45484be8496a140e_1_690x467.jpeg "Asteroids")

#### Adventure

### SD card menu

If you want multiple games on your console without having to upload them one at a time using the USB connector, you will need to use the SD card.
To do this you will need to solder wires between pins 32, 33, 24 and 35 and the TinyFPGA BX. But as the console already uses all the pins that are
available on the header, you will need to reuse existing pins. I used the pins that are connected to the direction buttons as these are not needed for
an SD card menu.

The SD card menu needs a new multiboot configuration so that the menu can write the hardware.bin file for the game to a new area in SPI flash that the Ice40 can then do a warm
boot from. The TinyFPGA, out of the box, has a multi-boot configuration with the bootloader at address a0 and the user image at address 0x28000. By default tinyprog
writes user data (firmeware.bin) to address 0x50000.

The first 160 (0xa0) bytes of SPI flash memory consists of 5 entries of 32 bytes which specify boot configurations. The first is for power-on boot and the other 4 are for warm boots.
The bootloader warms boots to the second warm boot configuration at address 0x28000. 

There is an icestorm tool, icemulti, which can set up multi-boot configuration, and is is this tool that produced the default TinyFPGA BX multiboot configuration.

To use the SD card menu you need to run icemult and specify all 4 warm configurations with the -a15 parameter to specify the displacement between configurations. This puts
the 4 warm boot configurations at addresses 0xa0 (for the boot loader), 0x28000 for the SD card menu or other user image , 0x50000, which is used for program code, not a hardware configuration, and
0x78000, which the SD card menu uses for the game's hardware configuration.

This means that when you reset or power-on the device, the bootloader boots from a0, and then warms boots the SD card menu from address 0x28000. The game only runs when you select
it from the SD card menu.

Having produced a new multiboot configuration, you need to get it into the SPI flash memory of your BX.

You could use tinyprog for that but you only get one shot at getting it right. If the write fails the bootloader will be corrupted and the BX will not boot.

The alternative is to use some sort of SPI programmer. There are various alternatives for that. One option is to use an Arduino sketch.

The option I took is to use another BX as the programmer. This needs you to rebuild a bootloader with "external" SPI pins. That is you change pins.pcg to use pins 1-4 as the SPOI pins rather than the "internal" omnes 29-32.

You can then run that modified bootloader as a user image and it will act as an SPI programmer for another BX (or other SPI flash device).

Whichever option you take for the SPI programmer, you need to attach wires to the SPI pins on the underside of the BX on the target device. I soldered breadboard wires to mine and removed 
them after I had changed the multiboot configuration.


 






















