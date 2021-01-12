# ProjectPSX

![psx](https://user-images.githubusercontent.com/28767885/60985122-30e29900-a33d-11e9-8956-4b933a2745b4.PNG)

**ProjectPSX is a C# coded emulator of the original Sony Playstation (Playstation 1/PS1/PSX)**

*This is a personal project with the scope to learn about hardware and the development of emulators.*

ProjectPSX dosn't use any external dependency and uses rather simplistic C# code.

At the moment the following is implemented:
- CPU (MIPS R3000A) with the Coprocessor 0 and Geometry Transformation Engine (GTE) Coprocessor.
- A BUS to interconnect the components.
- GPU with all the commands implemented with a software polygonal rasterizer.
- CDROM: Implemented the common commands.
- DMA transfers.
- Timers.
- Digital controller support (currently hardcoded to keyboard).
- A basic BIOS and MIPS disassembler.
- MDEC for video decoding 16/24 bpp FMV.
- Display Screen with 24 bpp support.
- Memory Card support.

What is not implemented (but should be...):
- DMA resumable transfers
- CDROM: Proper timmings.
- SPU

> **Note:**  A valid PlayStation Bios is needed to run the emulator. SCPH1001.BIN is the default bios on the development but some others like SCPH5501 or SCPH7001 have been reported to work.

## Compatibility

The emulator is in early development and there are constant rewrites. Somehow and although with some limitations there are some games that already "work" like:
Ridge Racer, Castlevania Symphony of the Night, Final Fantasy 7, Crash Bandicoot 1, 2 and 3, Spyro the dragon, Tekken 1, 2 and 3, Toshinden, Time Crisis, Tobal 1 and 2, Vagrant Story, Street Fighter Zero 3, Rockman/Megaman 8/X4, Parasite Eve...
Some others like Final Fantasy IX, Gran Turismo boot but have random problems to be fixed.

> **Note:**  Memory Card files are hardcoded to "memcard.mcr" on the root directory. If there's no one a new one will be generated on save.


## Using the emulator

Select a Bin file (use track1) or a Cue file to generate CD tracks to feed the CDROM.
The bios and expansion files are hardcoded on the BUS class
 
Once power on, Input is mapped as:

* D-Pad UP: **Up**
* D-Pad Left: **Left**
* D-Pad Down: **Down**
* D-Pad Right: **Right**
* Triangle: **W**
* Square: **A**
* X: **S**
* Circle: **D**
* Start: **Enter**
* Select: **Space**
* L1: **Q**
* R1: **E**
* L2: **1**
* R2: **2**

## Screenshots
![cpu](https://user-images.githubusercontent.com/28767885/60985112-304a0280-a33d-11e9-83b3-49a15fb1c117.PNG)
![gte](https://user-images.githubusercontent.com/28767885/60985120-30e29900-a33d-11e9-8cfa-1753b878e023.PNG)
![crash](https://user-images.githubusercontent.com/28767885/60985114-304a0280-a33d-11e9-80e2-08cd1c5abfbe.PNG)
![rr](https://user-images.githubusercontent.com/28767885/60985123-30e29900-a33d-11e9-9188-f942e44bcc3a.PNG)
![ff7](https://user-images.githubusercontent.com/28767885/60985116-304a0280-a33d-11e9-9944-f0dfc4f085c3.PNG)
![ff7B](https://user-images.githubusercontent.com/28767885/60985118-304a0280-a33d-11e9-9170-af6902f8bd08.PNG)

## Quick Faq
- Can i use this emulator to play?

Yes you can, but you shouldn't. There are a lot of other more capable emulators out there. This is a work in progress personal project with the aim to learn about emulators and hardware implementation. It can and will break during emulation as there are a lot of unimplemented hardware features.

- What's up with that window with all the weird colors and the double game screen?

It's the VRAM viewer. It includes all the textures, color lockup tables and display buffers used by the playstation software. It's used for debugging purposes. You can toggle it by pressing TAB on your keyboard.

- Why "insert game here" doesn't work?

Probably due to not implemented hardware or incorrect implemented one, mainly cdrom timmings.

- How can i get console TTY or BIOS output?

Uncomment the bios.verbose() or TTY() functions on the CPU main loop. You can also dissasemble() the MIPS CPU instructions and printRegs() on the current opcode.

- Why both RTPS and RTPT Geometry Transformation Engine Coprocessor commands give wrong values on tests?

At the moment i just use common division where the original PSX uses a fastest, but less accurate division mechanism (based on Unsigned Newton-Raphson (UNR) algorithm.

- Why you did this?

I have been interested in emulating hardware for some time. I started doing a Java [Chip8](https://github.com/BluestormDNA/Chip8) and a C# [Intel 8080 CPU](https://github.com/BluestormDNA/i8080-Space-Invaders) (used on the classic arcade Space Invaders). Some later i did [Nintendo Gameboy](https://github.com/BluestormDNA/ProjectDMG). I wanted to keep forward to do some 3D so i ended with the PSX as it had a good library of games...

- How you did this?

I  mainly used Martin Korth PSX-SPX documentation about the Playstation hardware at https://problemkaputt.de/psx-spx.htm
Also the people at the #playstation channel on the emudev discord at https://discord.gg/dkmJAes was very helpful.

- What about WinForms?

Winforms was the easiest way to have output for me as it was fast prototyped it somehow has lasted more than intended... but the idea is to let it go away in the future.
I looked at alternatives but as I said im more focused at the moment on the core aspect and not much on the UI. The WinForms dependency is very thin and can be easily changed (at some point i used GDI and even SDL).
Seems like .NET 5 will have a cross platform UI so maybe I will need to look onto that. Meanwhile I'm gonna create a branch with OpenToolkit and work on sound.

- Tell me more about you!

At the start of this project I was a guy with a boring job unrelated to coding. I did'nt want to do it for the rest of my life so I started studying to try to change careers. Eventually learned (a bit) and started to code whatever made me happy. Eventually got a job as an Android Dev...

