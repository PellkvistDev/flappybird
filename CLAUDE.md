# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file Flappy Bird game written in Swedish, playable directly in the browser. The entire game — HTML structure, CSS styling, and JavaScript logic — lives in `index.html`. There is no build step, package manager, test framework, or bundler.

To run: open `index.html` in any modern browser. No server required.

## Architecture

All game logic is in a single `<script>` block in `index.html`. The key globals:

- `bird` — object with position (`x`, `y`), physics (`gravity`, `lift`, `velocity`), and `radius`
- `pipes` — array of `{ x, top, bottom }` objects (pixel heights for top/bottom pipe sections)
- `frame` — tick counter; a new pipe spawns every 100 frames
- `score`, `gameOver` — game state flags

**Game loop** (`requestAnimationFrame`):
1. `update()` — advances physics, moves pipes left by 2.5px/frame, runs circle-vs-AABB collision detection, increments score when a pipe's x matches the bird's x
2. `draw()` — clears canvas, draws pipes with gradient fill + caps, draws the bird (rotated by velocity), overlays score and game-over screen

**Collision detection** uses the nearest-point-on-rect to circle-center distance formula, applied independently to the top and bottom pipe rectangles.

**Input**: `Space` keydown and canvas `mousedown` both set `bird.velocity = bird.lift` (flap) or call `resetGame()` if `gameOver` is true.

## Canvas dimensions

`320 × 480` px. Pipe gap is 130 px; pipe width is 50 px. Bird radius is 14 px. These constants are at the top of the script block.

## Language note

Comments and UI strings are in Swedish. Keep new comments in Swedish for consistency.
