# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

pMARS is a portable Memory Array Redcode Simulator - a Core War simulator that runs virus-like programs called "warriors" written in Redcode assembly language. This is version 0.9.2-5 of the simulator.

## Build System

The project uses a standard Makefile build system with the following commands:

### Build Commands
- `make` or `make all` - Build the main pmars executable
- `make clean` - Remove object files and clean build artifacts

### Current Build Configuration
The Makefile is currently configured with SDL2 graphics support with the following flags:
- `-DSDLGRAPHX` - Enables SDL2-based graphical core display
- `-DEXT94` - Enables ICWS'94 extensions (SEQ, SNE, NOP opcodes and addressing modes)
- `-DPERMUTATE` - Enables -P switch for permutation

The SDL graphics code has been successfully upgraded from SDL1 to SDL2 compatibility.

## Architecture

### Core Components
- **pmars.c** - Main entry point, initialization and cleanup
- **asm.c/asm.h** - Redcode assembler for parsing warrior source code
- **sim.c/sim.h** - Core War simulation engine
- **cdb.c** - Interactive debugger (when not compiled with -DSERVER)
- **disasm.c** - Disassembler for displaying Redcode instructions
- **eval.c** - Expression evaluator for assembler
- **pos.c** - Position handling utilities
- **global.c/global.h** - Global definitions and utilities
- **config.h** - Compile-time configuration options

### Display Modules
Multiple display backends are available depending on compile flags:
- **sdldisp.c** - SDL graphics display (currently active)
- **curdisp.c** - Curses text-based display
- **xwindisp.c** - X11 graphics display
- **lnxdisp.c** - Linux SVGA display
- **stddisp.c** - Standard text output

### Language Support
- **str_eng.c** - English language strings (template for localization)

## Configuration Options

Key preprocessor flags that control compilation (defined in config.h or via -D flags):

- `GRAPHX` - Enable platform-specific graphical core display
- `SERVER` - Disable debugger for non-interactive tournament mode
- `EXT94` - Enable ICWS'94 extensions and experimental opcodes
- `SMALLMEM` - Use 16-bit addresses to reduce memory footprint
- `SDLGRAPHX` - Use SDL for graphics (currently active)
- `XWINGRAPHX` - Use X11 for graphics
- `CURSESGRAPHX` - Use curses for text display

## File Extensions and Types

- `.c/.h` - C source and header files
- `.o` - Compiled object files (build artifacts)
- `pmars` - Main executable (no extension on Unix)
- `.red/.rc` - Redcode warrior source files (not in this repo)