# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-player Tic Tac Toe (human X vs AI O) delivered as one self-contained file: **`index.html`** (~390 lines of HTML + CSS + JS — no build tools, no dependencies, open directly in a browser).

## Running the game

Open `index.html` in any browser. No server or install step needed.

## Architecture

Everything lives in `index.html` in three clearly commented sections:

**CSS** (lines 7–143) — dark neon theme, all styles inline in `<style>`.  
Color palette: background `#1a1a2e`, cells `#16213e`/`#0f3460`, X = `#e94560` (red), O = `#4fc3f7` (blue), winner highlight `#f6e05e`.

**HTML** (lines 145–184) — static structure only. The 9 board cells are `<div class="cell" data-index="0..8">`. JS reads `data-index` to map DOM nodes to the flat `board` array.

**JavaScript** (lines 186–389) — no framework, no modules. Key pieces:

| Symbol | Purpose |
|--------|---------|
| `board` | `Array(9)` of `null \| 'X' \| 'O'` — single source of truth |
| `difficulty` | `'easy' \| 'medium' \| 'hard'` |
| `gameOver` | boolean; gates all click handlers |
| `score` | `{ X, draw, O }` — persists across rounds, resets on page refresh |
| `WIN_LINES` | constant array of the 8 winning triplets (rows, cols, diagonals) |
| `checkWinner(b)` | pure — returns `{ winner, line }` or `null` |
| `isDraw(b)` | pure — true when board is full and no winner |
| `renderBoard(winLine)` | rebuilds cell classes from `board` state; highlights `winLine` cells |
| `playerMove(index)` | places X, checks result, schedules `aiMove` via 300 ms `setTimeout` |
| `aiMove()` | dispatches to `aiEasy` / `aiMedium` / `aiHard` based on `difficulty` |
| `aiEasy(b)` | random empty cell |
| `aiMedium(b)` | win → block → random |
| `aiHard(b)` | full minimax (unbeatable) |
| `minimax(b, isMaximizing)` | recursive; scores: O win = +10, X win = −10, draw = 0 |
| `resetBoard()` | clears `board`, resets `gameOver`, re-renders; scores are **not** reset |

**Game flow:** player click → `playerMove` → optional `aiMove` (after 300 ms delay) → `endGame` locks board and updates score.  
Switching difficulty triggers `resetBoard` (board only, score preserved).

## Git workflow

Branch: `main` — push every meaningful change immediately.  
Commit format: `type: short present-tense description` (types: `feat`, `fix`, `refactor`, `style`, `chore`, `docs`).

```bash
git add .
git commit -m "type: description"
git push origin main
```
