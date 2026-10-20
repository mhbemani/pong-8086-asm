# pong-8086-asm

[![CI](https://github.com/mhbemani/pong-8086-asm/actions/workflows/ci.yml/badge.svg)](https://github.com/mhbemani/pong-8086-asm/actions/workflows/ci.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Pong written in 16-bit x86 assembly (NASM) for DOS, drawing directly to VGA mode 13h (320x200, 256 colors). One 880-line file, no libraries.

## Gameplay

- Move the paddle with the **left / right arrow keys**, quit with **Esc**
- The ball bounces off the walls, the ceiling, the paddle and the blocks
- Every paddle hit scores a point and changes the ball color; every 1-3 hits a new block appears at a random position, and a block takes 1-5 hits to destroy
- Reach a score of 30 to win; letting the ball fall ends the game

## Build and run

```
nasm -f bin pong.asm -o pong.com
```

Run `pong.com` in [DOSBox-X](https://dosbox-x.com/) (or any DOS emulator): mount the folder and type `pong`.

## How it is built

- `.COM` program (`org 0x100`), video through BIOS `int 10h`, keyboard through `int 16h`, random numbers from the BIOS tick counter (`int 1Ah`)
- Own routines for the border, paddle, ball, blocks, collision checks, and a bitmap-digit score display
- Timing is a busy-wait delay, so game speed depends on the emulator's CPU speed (adjust the cycles in DOSBox-X)
