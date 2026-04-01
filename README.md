# Sonick

A single-file, browser-playable 2D side-scrolling platform game built with vanilla JavaScript and the Canvas 2D API.

Live site: https://paulregnart.github.io/sonick/
Repository: https://github.com/paulregnart/sonick

## High-Level Game Overview

`sonick.html` implements a Sonic-inspired platformer featuring a porcupine hero named Sonick.

### Core gameplay loop

1. Move through a wide scrolling level.
2. Collect coins and avoid hazards.
3. Stomp eligible enemies for bonus coins.
4. Reach coin threshold for the current level.
5. Advance to a harder procedurally generated level.

### Player mechanics

- Arrow keys:
  - Left/Right: move
  - Up: jump and timed double jump
  - Down: duck/crouch
- Shift: run faster
- Smooth acceleration/deceleration physics
- Gravity, collision with ground/platforms, and ducking hitbox changes
- 3 lives, death animation, respawn invincibility, and Game Over state

### Progression and scoring

- Coin total is the main score
- Best score is persisted in `localStorage`
- Level goals scale by total coins (level number x 20)
- Level transitions increase difficulty (more enemies/platform pressure)

### World and hazards

- Procedurally generated levels (seeded by level number)
- Ground, platforms, stumps, spikes, and coin placements
- Obstacle overlap checks reduce unfair stacked hazards
- Camera follows player horizontally
- Parallax layers create depth

### Enemies

- Green and red monsters with behavior differences
- Some enemies can spawn on platforms and drop off naturally
- Improved steering/chasing and anti-stuck direction flips
- Alternating variants:
  - Pointy/horned enemies
  - Non-pointy enemies (stomp-killable)

### Audio and presentation

- Retro-style graphics drawn programmatically (no image assets)
- Web Audio API sound effects generated at runtime (no audio files)
- HUD for coins, best score, lives, and level
- Title, level complete, and game over overlays

## High-Level Code Overview

All logic lives in one file: `sonick.html`.

### Main sections in code

1. **Constants and configuration**
   - Canvas size, player tuning, difficulty presets, colors, storage keys.

2. **Utilities**
   - Math helpers (`clamp`, random helpers, overlap checks, seeded RNG).

3. **Canvas setup and responsive scaling**
   - Fixed internal resolution (800x450), CSS scaling to viewport.

4. **Audio system**
   - Web Audio context creation and procedural SFX helpers.

5. **Input handling**
   - Keyboard/mouse state with one-frame trigger flags (`justUp`, `justSpace`, etc.).

6. **Game state and player state**
   - Mode machine (`title`, `playing`, `dying`, `levelComplete`, `gameOver`).
   - Player physics/animation state.

7. **Procedural level generation**
   - Seeded generator for platforms, obstacles, coins, and enemies.
   - Difficulty and level scaling.

8. **Physics and collision**
   - Player movement, solid collisions, jump logic, spike death detection.

9. **Entities and interactions**
   - Coin collection + sparkle effects.
   - Enemy AI, movement, stomping, and damage rules.

10. **Camera and progression checks**
    - Horizontal camera follow and level complete trigger logic.

11. **Rendering pipeline**
    - Background/parallax, world geometry, enemies, player, HUD, overlays.

12. **Main loop**
    - `requestAnimationFrame` with fixed timestep simulation and frame delta cap.

## Controls

- `ArrowLeft` / `ArrowRight`: Move
- `ArrowUp`: Jump / Double jump (timed second press)
- `ArrowDown`: Duck
- `Shift`: Run
- `Space` or click: Start/restart on title/game over screens

## Run locally

Open `sonick.html` directly in Chrome (v146+) and play.

No build step, no dependencies, no external assets.
