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

This project was started by ![Discussion](https://discourse.tinyfpga.com/t/bx-portable-game-console-project-collaboration/553 "discussion") on the TinyFPGA forum.

### LCD Screen

The ![Games Console](https://www.buydisplay.com/default/2-8-inch-tft-touch-shield-for-arduino-w-capacitive-touch-screen-module "Games Console") used is a 320 x 240 screen
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

#### Space Invaders

Slightly more sophisticatede games such as Space Invaders could be implemented without a CPU, but it is hard to do that, and much easier using a CPU.

#### Pacman


#### Asteroids

### Pitfall

#### Adventure

#### Super Mario Bros

### Games consoles

#### Atari 2600

#### Nintendo NES

#### Nintendo SNES

#### Nintendo Gameboy















