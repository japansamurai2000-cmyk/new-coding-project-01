# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A collection of browser-playable games. Each game is a **single self-contained HTML file** — no build tools, no dependencies, no server required. Open any file directly in a browser to run it.

## Running Games

```bash
open tictactoe.html
open shooter.html
```

## Architecture

### Conventions (both games follow these)

- **Single file**: all HTML, CSS, and JS in one `.html` file.
- **Vanilla JS only**: no libraries, no frameworks, no imports.
- **Dark color palette**: background `#0a0a12` / `#0f0f1a`, accent purple `#c9b8ff`, monospace font (`Courier New`).
- **No build step**: files are committed and run as-is.

### shooter.html — Neon Assault

Canvas-based top-down shooter. Architecture:

- **`Game`** — orchestrator: RAF loop, state machine (`MENU → PLAYING → LEVEL_COMPLETE → WIN / GAME_OVER`), input handling, collision detection, spawn queue, screen shake.
- **`Player`** — movement (WASD/arrows), mouse aim angle, shooting with fire-rate timer, invincibility frames after damage.
- **`Enemy`** — all 6 types (`grunt`, `speeder`, `charger`, `shooter`, `tank`, `megatank`) share one class; behavior is driven by the `ETYPES` config object. Each type has its own `_draw*` method on Enemy.
- **`Bullet`** — shared for player and enemy projectiles (`fromPlayer` flag distinguishes them).
- **`Particle`** — lightweight struct, updated/filtered in a pool (cap 300).
- **`LEVELS`** array — 10 entries, each with `waves` (enemy type counts), `spMult`, `hpMult`, `delay`.

Sound uses inline `AudioContext` oscillators — no audio files.

### tictactoe.html

DOM-based (no canvas). State is a plain array + current player + score object. No classes.

## Git / GitHub

- Remote: `https://github.com/japansamurai2000-cmyk/new-coding-project-01`
- **After completing any meaningful unit of work, commit and push immediately.** This includes new features, bug fixes, refactors, and file additions. Never leave finished work uncommitted.
- Stage specific files by name (not `git add -A`) to avoid accidentally committing unrelated files.
- Commit messages should be concise and describe *what changed and why*, not just "update file".
- Always append the co-author line: `Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>`
- Always push after committing so GitHub reflects the current state of work.
