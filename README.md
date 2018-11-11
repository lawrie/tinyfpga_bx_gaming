# TinyFPGA BX Gaming

This repository documents how to use the TinyFPGA BX as a Games Console.

## Overview

A Field Programmable Gate Array (FPGA) is capable of emulating hardware such as an audio synthesizer, a Graphics Processing Unit (GPU), 
and drivers for devices such as a VGA screen or an Liquid Cyystal Display (LCD), game controllers, buttons, etc. It is also capable of implemented a CPU as a Soft Processor.

This means that an FPGA such as the TinyFPGA BX can replace all the chips used in games consoles or early home computers.

The approach taken is to to use the picorv32 implementation of Risc-V for the CPU that runs the games. However, it is also possible to use other soft processors,
such as a 6502 CPU or a Z80 CPU for specific games.

The TinyFPGA has the resources to emulate games consoles, arcade machines and home computers of the late 1970s, and early 1980s. The next generation of
open source FPGAs based on the ECP5 FPGA will be need for computers and consoles of the late 80s and early 90s.

I will concentate on a portable Games Console that drives a 320 by 240 LCD, but the code in the repositories referenced also supports TV games consoles driven by VGA.
Future implementations based on the ECP5 will support HDMI.

The hardware that I am using for portable Games console was produced by [Fabien Chouteau](https://github.com/Fabien-Chouteau/field-programmable-game-console).

![Games Console](https://discourse.tinyfpga.com/uploads/default/original/1X/5a128efae7be41d5a157ea954480067cdb7e602e.jpeg "Games Console")

The TinyFPGA BX has 16kb of BRAM, or which 2kb is used by picorv32. This allows a RAM-only version of PicoSoC to be used that has 14kb of RAM for the code, data,
and video RAM. This is sufficient for emulating early consoles such as the Atari 2600.

The TinyFPGA also has 1 Mb of flash memory. A significant fraction is available for executing code from. So a version of PicoSoC can be produced that runs the code 
from flash memory allowing much bigger programs, but still limiting VGA buffers and writeable data to 14kb.

This project was started by Discussion](https://discourse.tinyfpga.com/t/bx-portable-game-console-project-collaboration/553) on the TinyFPGA forum.

### LCD Screen

The [LCD Screen](https://www.buydisplay.com/default/2-8-inch-tft-touch-shield-for-arduino-w-capacitive-touch-screen-module) used is a 320 x 240 screen
using the 8-bit 8080 driver and without any touchscreen option.

### Audio

The audio is based on Dave Gundy's tiny-synth project which implements an audio synthesizer similar to the Commodore C64 SID chip.

## History of Gaming

### Classic Games

#### Pong

The earliest video games such as Pong and Space Invaders were implemented on dedicated Arcade machines, or dedicated hardware that plugged into a TV, such as the Atari Pong machine.

Pong is such a simple game that it can be implemented on an FPGA without using a CPU. Here is my port of the Pong game from the fpga4fun site, running on the Tiny FPGA BX.
It uses a rotary encoder to control the board and uses VGA output. It is not the full pong games as it only has one player, and does not show the score, but could 	easily be
modified to be more like the original pong game.

![Fpga4fun Pong](https://discourse.tinyfpga.com/uploads/default/original/1X/e4ccbf25da97bfff96cda172fdfdac4a033995c4.jpg "Fpga4fun Pong")

#### Space Invaders

Slightly more sophisticatede games such as Space Invaders could be implemented without a CPU, but it is hard to do that, and much easier using a CPU.

#### Pacman

#### Asteroids

#### Adventure

### Pitfall and other Atari 2600 games

#### Super Mario Bros

#### Tetris

#### Mario Kart

### Games consoles

#### Atari 2600

#### Nintendo NES

#### Nintendo SNES

#### Nintendo Gameboy

### Graphics Processing Units

What are now called Graphics Processing Units started life as very simple devices to support writing to TV screens using minimals resource such as RAM and CPU time.

#### Apple One

The Apple One computer had an extremely simple chip for driving the TV. There is an implementation of the Apple One on the TinyFPGA BX.

#### Atari TIA

Another early example is the Television Interface Adapter (TIA) used by the Atari 2600.

#### NES Picture Processing Unit (PPU)

### Home Computers

#### Apple One

#### Sinclair ZX Sprecturm

#### Acorn Atom and BBC Micro

#### Commodore C64

#### Commodore Amiga

## Building your own version

### The hardware

You will need a TinyFPGA BX, which can be bought from a variety of sources including Tindie, Sparkfun and Amazon UK.

To build the portable version you will need to get a version of Fabien Chouseau's PCB or build your own.

There are not many components on the PCB. There are the headers for the TintFPGA and the LCD screen, connectors for the batteries,
a switch and an audio connector. There are also 7 SMD passive devices: 4 capacitors, 2 resistors and a diode.

You will also need the LCD screen.

### Unix machine or VM

You will need a Unix machine to build the software. This can be a MAC or a Linux box, or a VM on a Windows machine. 

You should install the TinyFPGA tools and the picov32 GNU compiler.

### Games

There are a variety of games that you can build for the console, or you can write your own.

#### Dave Gundy's demo

#### Pacman

#### Tetris 

#### Super Mario Bros

#### Asteroids

#### Adventure

### SD card menu

If you want multiple games on your console without having to upload them one at a time using the USB connector, you will need to iuse the SD card.
To do this you will need to solder wires between pins 32, 33, 24 and 35 




















