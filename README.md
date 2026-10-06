# Frostkeep

A neon ice-castle rhythm runner for the browser. One touch, five checkpoints.

Your lime cube auto-runs through a frozen keep to a 140 BPM synth track. Jump the crystal spikes, bounce off amber pads, and tap orbs in mid-air. Pink gates turn you into a sled-ship you fly by holding.

The difficulty ramps gently: the opening is single spikes with plenty of room, and controls are forgiving (see below).

**Play it:** https://15june.github.io/frostkeep/

## Controls

| Action | Touch | Keyboard / mouse |
| --- | --- | --- |
| Jump (hold to keep jumping) | Tap / hold | Space, Up, W, Enter, or click |
| Rise in ship mode | Hold | Hold any jump key |
| Pause | Pause button | Esc or P |
| Restart from 0% | Pause > Restart level | R |

## Features

- Single ~54-second level with progress bar, attempt counter and best % saved in the browser
- Forgiving controls: a tap just before landing still jumps (jump buffer), you can jump a moment after leaving a ledge (coyote time), and spike hitboxes are slimmer than they look
- Five checkpoint flags: crash and you respawn at the last flag you passed (with a short get-ready pause), not the start. Each flag was verified beatable from its respawn point
- Practice mode adds frequent automatic checkpoints on top of the flags
- Procedural Web Audio soundtrack that restarts with every attempt, plus mute toggle
- Mobile friendly, best in landscape. Portrait shows a rotate prompt (with a "play anyway" option). Android can go fullscreen and lock to landscape
- No build step and no dependencies: everything lives in `index.html`

## Run locally

Open `index.html` in any modern browser. That's it.

## Under the hood

- `CORE` (top of the script) holds the level layout and a deterministic fixed-step physics engine (240 Hz).
- The level was verified beatable by a search bot that runs the same physics, and every jump was measured to have at least a 167 ms timing window (183 ms or more in the first 30%).
- Rendering is a single `<canvas>` with pre-rendered sprites for performance on phones.

### Editing the level

Level objects are placed in `buildLevel()` using small helpers:

- `S(x, y)` spike, `SR(x, n)` row of spikes, `SD(x, y)` hanging spike
- `B(x, y, w, h)` block
- `P(x)` jump pad, `O(x, y)` jump orb
- `GATE(x, 'ship' | 'cube')` mode gate
- `CP(x, mode, y)` checkpoint flag (respawn point)

Units are blocks; the player moves 9 blocks per second.
