# Project Knowledge Base: Hot Icarus Game ("ICARUS INC.")

This knowledge base represents the current architecture, tech stack, and gameplay mechanics of the Hot Icarus Game. Read it before writing any code or making visual modifications.

---

## What this project is

**ICARUS INC.** is a retro-style, 2D pixel-art vertical arcade game. The player controls a winged hero ascending toward a massive sun, dodging obstacles, and shooting down falling hazards. 

---

## Technical Stack & Architecture

- **Vanilla HTML5 Canvas**: The entire game is built with zero external dependencies, written in vanilla HTML, CSS, and JavaScript.
- **Monolithic File**: All gameplay logic, canvas drawing, styles, and markup reside in [game.html](file:///Users/emilychai/hot-icarus-playground/game.html).
- **Pixel-Art Render Engine**: 
  - The game uses a low-resolution offscreen buffer canvas of `128x224` pixels for rendering.
  - Everything is drawn directly onto this offscreen buffer to achieve authentic pixel-art detail.
  - The offscreen buffer is scaled up to the visible `256x448` canvas using `ctx.drawImage` with `imageSmoothingEnabled = false` (nearest-neighbor scaling).
  - A post-processing pass applies CRT scanlines and a dark vignette overlay directly to the buffer.
- **Procedural Graphics**: All sprites (player, fireballs, stars, hearts) are rendered procedurally using 2D canvas drawing methods (`fillRect`, `arc`, etc.). This ensures zero-dependency local running (no CORS or image loading errors).

---

## Folder Structure

```
/Users/emilychai/hot-icarus-playground/
  ├── game.html                      # Core game file (HTML, CSS, JS)
  └── antigravity-knowledge-base.md   # This project knowledge base
```

---

## Core Gameplay Mechanics

1. **Controls**:
   - `Left / Right Arrow`: Move horizontally.
   - `Up Arrow`: Climb up towards the Sun (subject to gravity when released).
   - `Spacebar`: Shoot projectiles upward.
   - `Enter`: Start or restart the game.
2. **Win Condition**: Reach the Sun line (`y <= 70` in canvas coordinates). Completing a level increments the level up to a maximum of 10, increasing difficulty.
3. **Obstacles & Hazards**:
   - **Fireballs**: Fall from the top of the screen at speeds scaling with level. Can be shot down for score points (+10).
   - **Lightning Bolts**: Periodic warnings followed by a massive, high-speed vertical lightning strike targeting a randomized column.
4. **Player Stats**:
   - High Score (stored in `localStorage`).
   - Current Score.
   - Health (5 HP, represented by retro pixel hearts, with temporary invulnerability frames on hit).

