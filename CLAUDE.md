# NeonBreaker - Project Instructions

## What This Is
NeonBreaker is a single-file Arkanoid/Breakout PWA game. Target audience: friends playing on iPhones from home screen. It's a fun personal project with Ozan Selcuk easter eggs throughout.

## Architecture
- **Single file game**: Everything is in `index.html` (inline CSS + JS in an IIFE)
- **PWA files**: `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`
- **Hosted**: GitHub Pages at https://ozan2025.github.io/NeonBreaker/
- **Repo**: https://github.com/ozan2025/NeonBreaker

## Game Constants
- Logical canvas: 480x800, scaled with letterboxing
- 12-column x 20-row brick grid
- Level grids use chars: `.`=empty, `1`=normal, `2`=tough, `3`=armored, `X`=explosive, `#`=indestructible
- 10 levels, 11 power-ups, 250 particle pool

## When Making Changes
- Bump the version string on the start screen (search for `'v3'` or current version)
- Bump `CACHE_NAME` in `sw.js` if you want existing PWA installs to update
- After changes: `git add index.html && git commit && git push` — GitHub Pages auto-deploys
- Test on mobile viewport (375x812) and desktop — game must scale to both
- All game state is in the `G` object inside the IIFE — not accessible from console

## Touch Controls
- Uses **frame-by-frame delta** tracking (not absolute position)
- The `1.4` multiplier on touch delta makes it feel responsive
- Do NOT change back to absolute-delta — it caused corner-sticking bugs

## Ozan Easter Eggs
These are intentional and should be preserved:
- Start screen: "An Ozan Selcuk Production" credit
- Level names with Ozan references
- Fireball popup, combo messages, game over quips, victory message
- See `OZAN_QUIPS` array and `ozanCombo` array in code

## Sounds
All synthesized via Web Audio API — no audio files. `initAudio()` is called lazily on first user gesture. `muted` flag + `masterGain` control volume.

## Don't Break
- Offline functionality (SW caching)
- Touch controls (delta-based, not position-based)
- The IIFE wrapper (prevents global pollution)
- Power-up timer display (uses explicit `effectMap`, not index-based)
- `G.beaten` flag (distinguishes victory from game-over)
