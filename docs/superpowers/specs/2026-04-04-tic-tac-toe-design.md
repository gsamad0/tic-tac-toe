# Tic Tac Toe — Design Spec

**Date:** 2026-04-04

## Overview

A browser-playable Tic Tac Toe game delivered as a single self-contained `index.html` file. No build tools, no server required — open the file in any browser to play.

## Game Mode

Single player: human (X) vs AI (O). Human always goes first.

## Difficulty Levels

Three modes selectable via pill buttons at the top of the game:

- **Easy** — AI picks a random empty cell each turn.
- **Medium** — AI wins immediately if it can; blocks the player from winning if it must; otherwise picks randomly.
- **Hard** — AI uses full minimax algorithm (unbeatable — always draws or wins).

Switching difficulty resets the current board but preserves the score tracker.

## Visual Style

Dark Neon theme:

- Background: `#1a1a2e`
- Board cells: `#16213e` with `#0f3460` borders
- X color: `#e94560` (neon red)
- O color: `#4fc3f7` (neon blue)
- Active difficulty pill: neon red highlight
- Status text: neon blue
- Font: system sans-serif; monospace not required

## Layout (top to bottom)

1. **Title** — "TIC TAC TOE" in neon red, uppercase, letter-spaced
2. **Difficulty selector** — Easy / Medium / Hard pill buttons; active one highlighted
3. **Status line** — dynamic text: "Your turn", "AI thinking...", "You win!", "AI wins!", "It's a draw!"
4. **3×3 Board** — 80×80px cells, 8px gap, hover glow on empty cells
5. **Score tracker** — You (X) / Draws / AI (O); persists across rounds within a session
6. **New Game button** — resets board only; scores carry over

## Game Flow

1. Page loads → Easy difficulty selected by default, empty board, score at 0-0-0.
2. Player clicks an empty cell → X placed, cell no longer clickable.
3. Win/draw check runs immediately after each move.
4. If game continues, AI takes its turn (brief 300ms delay to feel natural), places O.
5. Win/draw check runs again.
6. On game end: status line updates with result; winning cells highlighted; board becomes non-interactive.
7. Player clicks "New Game" → board clears, same difficulty stays active, scores persist.

## Win Detection

Check all 8 lines after every move: 3 rows, 3 columns, 2 diagonals. If all three cells in a line belong to the same player, that player wins. If all 9 cells are filled with no winner, it's a draw.

## AI Implementation

### Easy
```
pick a random cell from the list of empty cells
```

### Medium
```
1. if AI can win in one move → take it
2. else if player can win in one move → block it
3. else → pick randomly
```

### Hard
Full minimax with no depth limit (board is small enough — max 9 levels deep):
```
minimax(board, isMaximizing):
  if terminal state → return score (+10 AI win, -10 player win, 0 draw)
  if isMaximizing:
    return max score over all empty cells
  else:
    return min score over all empty cells
```

## File Structure

```
index.html          ← entire game (HTML + CSS + JS, ~300 lines)
docs/
  superpowers/
    specs/
      2026-04-04-tic-tac-toe-design.md
```

## Out of Scope

- Multiplayer (two players, online or pass-and-play)
- Animations beyond cell hover glow and win highlight
- Sound effects
- Mobile-specific optimizations (game is usable on desktop browsers)
- Persistent score storage (scores reset on page refresh)
