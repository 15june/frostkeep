# Frostkeep

A neon ice-castle rhythm runner for the browser. One touch, no second chances.

Your lime cube auto-runs through a frozen keep to a 140 BPM synth track. Jump the crystal spikes, bounce off amber pads, and tap orbs in mid-air. Pink gates turn you into a sled-ship you fly by holding.

**Play it:** https://15june.github.io/frostkeep/ (once GitHub Pages is on, see below)

## Controls

| Action | Touch | Keyboard / mouse |
| --- | --- | --- |
| Jump (hold to keep jumping) | Tap / hold | Space, Up, W, Enter, or click |
| Rise in ship mode | Hold | Hold any jump key |
| Pause | Pause button | Esc or P |
| Restart | Pause > Restart | R |

## Features

- Single 46-second level with progress bar, attempt counter and best % saved in the browser
- Practice mode with automatic checkpoints
- Procedural Web Audio soundtrack that restarts with every attempt, plus mute toggle
- Mobile friendly, best in landscape. Portrait shows a rotate prompt (with a "play anyway" option). Android can go fullscreen and lock to landscape
- No build step and no dependencies: everything lives in `index.html`

## Run locally

Open `index.html` in any modern browser. That's it.

## Host on GitHub Pages

1. Go to **Settings > Pages** in this repo.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. Save. The game will be live at `https://15june.github.io/frostkeep/` within a minute or two.

## Under the hood

- `CORE` (top of the script) holds the level layout and a deterministic fixed-step physics engine (240 Hz).
- The level was verified beatable by a search bot that runs the same physics, so no jump needs frame-perfect timing.
- Rendering is a single `<canvas>` with pre-rendered sprites for performance on phones.

### Editing the level

Level objects are placed in `buildLevel()` using small helpers:

- `S(x, y)` spike, `SR(x, n)` row of spikes, `SD(x, y)` hanging spike
- `B(x, y, w, h)` block
- `P(x)` jump pad, `O(x, y)` jump orb
- `GATE(x, 'ship' | 'cube')` mode gate

Units are blocks; the player moves 10.4 blocks per second.
