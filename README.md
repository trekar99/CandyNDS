# CandyNDS

CandyNDS is a Candy Crush-style match-3 game developed for the Nintendo DS (NDS). It was created as a Computer Architecture practice project for the 2nd year of the Computer Engineering degree at the Universitat Rovira i Virgili (URV).

## Project Overview

The game is played on a 6x8 grid. The player swaps adjacent elements on the touchscreen to create sequences of 3 or more identical elements in a row or column. Each level has a specific point objective, a limited number of moves, and a set of jellies that must be cleared. The game progresses through 9 levels of increasing difficulty.

## Authors

- Main analyst-programmer: santiago.romani@urv.cat
- Auxiliary analyst-programmer: pere.millan@urv.cat
- Programmer 1: sergi.llobet@estudiants.urv.cat
- Programmer 2: germanangel.puerto@estudiants.urv.cat
- Programmer 3: jaume.tello@estudiants.urv.cat
- Programmer 4: ivan.garciap@estudiants.urv.cat

## Requirements

To build and run this project, the following tools must be installed and configured:

- [devkitARM](https://devkitpro.org/wiki/Getting_Started) - ARM cross-compiler toolchain for Nintendo DS development
- [devkitPRO](https://devkitpro.org/) - Provides libnds and other Nintendo DS libraries
- [DeSmuME](https://desmume.org/) - Nintendo DS emulator, used for running and debugging

The following environment variables must be set before building:

```
export DEVKITARM=<path to devkitARM>
export DEVKITPRO=<path to devkitPRO>
export DESMUME=<path to DeSmuME>
```

## Project Structure

```
CandyNDS/
  source/         - C and ARM assembly source files
  include/        - Header files and include definitions
  graphics/       - Graphic tile and background data (ARM assembly)
  audio/          - Audio samples (WAV files)
  Makefile        - Build configuration
```

### Source Files

| File | Description |
|---|---|
| candy2_main.c | Main game loop and initialization |
| candy2_graf.c | Graphics initialization and rendering |
| candy2_sopo.c | Support functions for graphical mode |
| candy2_supo.s | Low-level assembly support for graphics |
| candy2_conf.s | Level configuration data |
| candy1_init.s | Matrix initialization and element recombination |
| candy1_secu.s | Sequence detection and elimination |
| candy1_move.s | Element movement and falling logic |
| candy1_comb.s | Combination detection and suggestions |
| RSI_timer0.s | Timer 0 interrupt handler (element movement) |
| RSI_timer1.s | Timer 1 interrupt handler |
| RSI_timer2.s | Timer 2 interrupt handler (jelly animation) |
| RSI_timer3.s | Timer 3 interrupt handler (background scrolling) |
| Sprites_sopo.s | Sprite support routines |

## Building

To build the project, run:

```
make
```

This will compile all source files and produce a `candyNDS.nds` ROM file.

To clean all intermediate and output files:

```
make clean
```

## Running and Debugging

To run the game in DeSmuME:

```
make run
```

To run the game in debug mode (using DeSmuME with GDB over TCP port 1000):

```
make debug
```

## Gameplay

### Controls

| Input | Action |
|---|---|
| Touchscreen drag | Swap two adjacent elements |
| Button A | Confirm level transition (next level, repeat, or reshuffle) |
| Button X | Toggle background music on/off |
| Button Y | Toggle background scrolling on/off |

### Objective

Each level requires the player to:

1. Clear all jellies on the board.
2. Reach or exceed a target point score.
3. Complete both goals within the allowed number of moves.

If the player runs out of moves without clearing all jellies, the level must be repeated. If no valid moves remain, the board is automatically reshuffled.

### Scoring

| Match Type | Points |
|---|---|
| Sequence of 3 elements | 30 |
| Sequence of 4 elements | 60 |
| Sequence of 5 elements | 120 |
| Combination of 5 elements | 150 |
| Combination of 6 elements | 200 |
| Combination of 7 elements | 300 |

### Hints

If the player is idle for approximately 8 seconds, the game will suggest a valid move by animating a possible combination on the board.

## Levels

The game contains 9 levels (0 through 8). Each level has its own board layout, point objective, maximum number of moves, and number of jellies to clear.

## License

This project was developed for academic purposes at the Universitat Rovira i Virgili (URV). All rights reserved by the respective authors.
