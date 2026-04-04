# Tic Tac Toe Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single self-contained `index.html` Tic Tac Toe game with 3 AI difficulty levels and a dark neon visual theme.

**Architecture:** All HTML, CSS, and JavaScript live in one file. Game logic is written as pure functions (no DOM dependencies) so they can be tested in the browser console with simple assertions. The UI layer calls these functions and updates the DOM.

**Tech Stack:** Vanilla HTML5, CSS3, JavaScript (ES6). No libraries, no build tools. Open `index.html` directly in a browser.

---

## File Map

| File | Action | Responsibility |
|------|--------|---------------|
| `index.html` | Create | Entire game — HTML structure, CSS theme, JS game logic + UI |

---

### Task 1: HTML skeleton + Dark Neon CSS

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with full structure and CSS**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: #1a1a2e;
      color: #e2e8f0;
      font-family: system-ui, -apple-system, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      gap: 24px;
      padding: 24px;
    }

    h1 {
      color: #e94560;
      font-size: 32px;
      letter-spacing: 6px;
      text-transform: uppercase;
    }

    /* Difficulty pills */
    #difficulty {
      display: flex;
      gap: 10px;
    }

    #difficulty button {
      background: #0f3460;
      color: #a0aec0;
      border: 1px solid #0f3460;
      padding: 6px 20px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 14px;
      transition: all 0.15s;
    }

    #difficulty button.active {
      background: #e94560;
      border-color: #e94560;
      color: #fff;
    }

    /* Status */
    #status {
      color: #4fc3f7;
      font-size: 16px;
      letter-spacing: 1px;
      height: 24px;
    }

    /* Board */
    #board {
      display: grid;
      grid-template-columns: repeat(3, 80px);
      grid-template-rows: repeat(3, 80px);
      gap: 8px;
    }

    .cell {
      background: #16213e;
      border: 2px solid #0f3460;
      border-radius: 6px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 40px;
      font-weight: bold;
      cursor: pointer;
      transition: border-color 0.15s, box-shadow 0.15s;
      user-select: none;
    }

    .cell:hover:not(.taken):not(.locked) {
      border-color: #4fc3f7;
      box-shadow: 0 0 10px rgba(79, 195, 247, 0.3);
    }

    .cell.x { color: #e94560; cursor: default; }
    .cell.o { color: #4fc3f7; cursor: default; }
    .cell.taken { cursor: default; }
    .cell.locked { cursor: default; }

    .cell.winner {
      border-color: #f6e05e;
      box-shadow: 0 0 16px rgba(246, 224, 94, 0.5);
    }

    /* Score */
    #score {
      display: flex;
      gap: 32px;
      align-items: center;
    }

    .score-item {
      text-align: center;
    }

    .score-value {
      font-size: 28px;
      font-weight: bold;
    }

    .score-value.x { color: #e94560; }
    .score-value.draw { color: #a0aec0; }
    .score-value.o { color: #4fc3f7; }

    .score-label {
      color: #a0aec0;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-top: 4px;
    }

    /* New game button */
    #new-game {
      background: transparent;
      color: #a0aec0;
      border: 1px solid #0f3460;
      padding: 8px 28px;
      border-radius: 20px;
      cursor: pointer;
      font-size: 14px;
      letter-spacing: 1px;
      transition: border-color 0.15s, color 0.15s;
    }

    #new-game:hover {
      border-color: #4fc3f7;
      color: #4fc3f7;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>

  <div id="difficulty">
    <button class="active" data-level="easy">Easy</button>
    <button data-level="medium">Medium</button>
    <button data-level="hard">Hard</button>
  </div>

  <div id="status">Your turn</div>

  <div id="board">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>

  <div id="score">
    <div class="score-item">
      <div class="score-value x" id="score-x">0</div>
      <div class="score-label">You (X)</div>
    </div>
    <div class="score-item">
      <div class="score-value draw" id="score-draw">0</div>
      <div class="score-label">Draws</div>
    </div>
    <div class="score-item">
      <div class="score-value o" id="score-o">0</div>
      <div class="score-label">AI (O)</div>
    </div>
  </div>

  <button id="new-game">New Game</button>

  <script>
    // JS will go here in later tasks
  </script>
</body>
</html>
```

- [ ] **Step 2: Open `index.html` in a browser**

Double-click the file to open it. Verify:
- Dark background (`#1a1a2e`), neon red title
- Three difficulty pills (Easy highlighted in red)
- 3×3 grid of dark cells
- Score tracker showing 0 / 0 / 0
- "New Game" button visible
- Hovering a cell shows a blue glow border

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: HTML skeleton and dark neon CSS"
```

---

### Task 2: Game state + board rendering

**Files:**
- Modify: `index.html` — replace the `<script>` block

- [ ] **Step 1: Add game state and renderBoard function**

Replace `// JS will go here in later tasks` inside the `<script>` tag with:

```javascript
// ─── State ───────────────────────────────────────────────────────────────────
let board = Array(9).fill(null);   // null | 'X' | 'O'
let difficulty = 'easy';
let gameOver = false;
const score = { X: 0, draw: 0, O: 0 };

// ─── DOM refs ────────────────────────────────────────────────────────────────
const cells = document.querySelectorAll('.cell');
const statusEl = document.getElementById('status');
const scoreXEl = document.getElementById('score-x');
const scoreDrawEl = document.getElementById('score-draw');
const scoreOEl = document.getElementById('score-o');

// ─── Render ──────────────────────────────────────────────────────────────────
function renderBoard(winLine = []) {
  cells.forEach((cell, i) => {
    const val = board[i];
    cell.textContent = val ?? '';
    cell.className = 'cell';
    if (val === 'X') cell.classList.add('x', 'taken');
    if (val === 'O') cell.classList.add('o', 'taken');
    if (gameOver) cell.classList.add('locked');
    if (winLine.includes(i)) cell.classList.add('winner');
  });
}

function renderScore() {
  scoreXEl.textContent = score.X;
  scoreDrawEl.textContent = score.draw;
  scoreOEl.textContent = score.O;
}

// Initial render
renderBoard();
renderScore();
```

- [ ] **Step 2: Verify in browser console**

Open DevTools → Console and run:
```javascript
board[0] = 'X'; renderBoard();
```
Cell 0 should show a red X. Then run:
```javascript
board[0] = null; renderBoard();
```
Cell 0 should be empty again.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: game state and board rendering"
```

---

### Task 3: Win/draw detection

**Files:**
- Modify: `index.html` — add pure logic functions to `<script>`

- [ ] **Step 1: Add `checkWinner` and `isDraw` functions**

Add after `renderScore()` (before `// Initial render`):

```javascript
// ─── Game logic (pure functions) ─────────────────────────────────────────────
const WIN_LINES = [
  [0,1,2],[3,4,5],[6,7,8],   // rows
  [0,3,6],[1,4,7],[2,5,8],   // columns
  [0,4,8],[2,4,6]            // diagonals
];

// Returns { winner: 'X'|'O', line: [i,j,k] } or null
function checkWinner(b) {
  for (const line of WIN_LINES) {
    const [a, bb, c] = line;
    if (b[a] && b[a] === b[bb] && b[a] === b[c]) {
      return { winner: b[a], line };
    }
  }
  return null;
}

// Returns true if board is full with no winner
function isDraw(b) {
  return b.every(cell => cell !== null) && !checkWinner(b);
}
```

- [ ] **Step 2: Test in browser console**

Open DevTools → Console and run these assertions:

```javascript
// Should return null (empty board)
console.assert(checkWinner(Array(9).fill(null)) === null, 'empty board: no winner');

// X wins top row
const b1 = ['X','X','X',null,null,null,null,null,null];
const r1 = checkWinner(b1);
console.assert(r1?.winner === 'X', 'X wins row 0');
console.assert(JSON.stringify(r1?.line) === '[0,1,2]', 'correct win line');

// O wins left column
const b2 = ['O',null,null,'O',null,null,'O',null,null];
const r2 = checkWinner(b2);
console.assert(r2?.winner === 'O', 'O wins col 0');

// Diagonal win
const b3 = ['X',null,null,null,'X',null,null,null,'X'];
console.assert(checkWinner(b3)?.winner === 'X', 'X wins diagonal');

// Draw
const b4 = ['X','O','X','X','O','X','O','X','O'];
console.assert(isDraw(b4) === true, 'draw detected');

// Not a draw — game still in progress
const b5 = ['X','O','X','X','O','X','O',null,null];
console.assert(isDraw(b5) === false, 'not a draw yet');

console.log('All win/draw tests passed');
```

All assertions should pass with no errors logged.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: win and draw detection logic"
```

---

### Task 4: Player click handling + game loop

**Files:**
- Modify: `index.html` — add click handler and `endGame` / `startTurn` to `<script>`

- [ ] **Step 1: Add `endGame`, `playerMove`, and click wiring**

Add after the `isDraw` function:

```javascript
// ─── Game flow ────────────────────────────────────────────────────────────────
function endGame(result) {
  // result: 'X' | 'O' | 'draw'
  gameOver = true;
  const winResult = checkWinner(board);
  renderBoard(winResult ? winResult.line : []);
  if (result === 'X') {
    score.X++;
    statusEl.textContent = 'You win!';
  } else if (result === 'O') {
    score.O++;
    statusEl.textContent = 'AI wins!';
  } else {
    score.draw++;
    statusEl.textContent = "It's a draw!";
  }
  renderScore();
}

function playerMove(index) {
  if (gameOver || board[index]) return;
  board[index] = 'X';
  renderBoard();
  const win = checkWinner(board);
  if (win) { endGame('X'); return; }
  if (isDraw(board)) { endGame('draw'); return; }
  statusEl.textContent = 'AI thinking...';
  // AI move added in next task
}

// Wire up cell clicks
cells.forEach(cell => {
  cell.addEventListener('click', () => {
    playerMove(Number(cell.dataset.index));
  });
});
```

- [ ] **Step 2: Verify in browser**

Click any empty cell — it should show a red X. Click an occupied cell — nothing happens. The status line should read "AI thinking..." after your move (AI not yet implemented — that's fine).

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: player click handling and game-over detection"
```

---

### Task 5: Easy AI

**Files:**
- Modify: `index.html` — add AI functions and hook into `playerMove`

- [ ] **Step 1: Add `getEmptyCells`, `aiEasy`, and `aiMove`**

Add after the `playerMove` function (before the click wiring):

```javascript
// ─── AI ──────────────────────────────────────────────────────────────────────
function getEmptyCells(b) {
  return b.reduce((acc, val, i) => (val === null ? [...acc, i] : acc), []);
}

function aiEasy(b) {
  const empty = getEmptyCells(b);
  return empty[Math.floor(Math.random() * empty.length)];
}

function aiMove() {
  let index;
  if (difficulty === 'easy') index = aiEasy(board);
  // medium and hard added in later tasks
  board[index] = 'O';
  renderBoard();
  const win = checkWinner(board);
  if (win) { endGame('O'); return; }
  if (isDraw(board)) { endGame('draw'); return; }
  statusEl.textContent = 'Your turn';
}
```

- [ ] **Step 2: Wire `aiMove` into `playerMove`**

In `playerMove`, replace the comment `// AI move added in next task` with:

```javascript
setTimeout(aiMove, 300);
```

- [ ] **Step 3: Verify in browser**

Play a game on Easy — the AI should respond after ~300ms with a random O. Play to a win, loss, or draw and verify the status and score update correctly.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: easy AI (random move)"
```

---

### Task 6: Medium AI

**Files:**
- Modify: `index.html` — add `aiMedium` and update `aiMove`

- [ ] **Step 1: Add `findWinningMove` helper and `aiMedium`**

Add after `aiEasy`:

```javascript
// Returns the index of a winning move for `player`, or null
function findWinningMove(b, player) {
  for (const line of WIN_LINES) {
    const [a, bb, c] = line;
    const vals = [b[a], b[bb], b[c]];
    const playerCount = vals.filter(v => v === player).length;
    const emptyCount = vals.filter(v => v === null).length;
    if (playerCount === 2 && emptyCount === 1) {
      return line[vals.indexOf(null)];
    }
  }
  return null;
}

function aiMedium(b) {
  // Win if possible
  const win = findWinningMove(b, 'O');
  if (win !== null) return win;
  // Block player win
  const block = findWinningMove(b, 'X');
  if (block !== null) return block;
  // Otherwise random
  return aiEasy(b);
}
```

- [ ] **Step 2: Update `aiMove` to call `aiMedium`**

In `aiMove`, change the if/else block to:

```javascript
if (difficulty === 'easy') index = aiEasy(board);
else if (difficulty === 'medium') index = aiMedium(board);
// hard added in next task
```

- [ ] **Step 3: Test `findWinningMove` in browser console**

```javascript
// AI (O) can win by placing at index 2
const bWin = ['O','O',null,null,null,null,null,null,null];
console.assert(findWinningMove(bWin, 'O') === 2, 'AI wins at index 2');

// Player (X) about to win — AI should block at index 8
const bBlock = ['X','X',null,null,null,null,null,null,null];
// findWinningMove for X returns 2, so AI blocks 2
console.assert(findWinningMove(bBlock, 'X') === 2, 'blocks player at index 2');

// No winning/blocking move available
const bNone = ['X','O',null,null,null,null,null,null,null];
console.assert(findWinningMove(bNone, 'O') === null, 'no winning move');

console.log('Medium AI tests passed');
```

- [ ] **Step 4: Switch to Medium and play a game**

Switch to Medium difficulty. Verify:
- AI takes a winning move when available
- AI blocks you when you're one move from winning
- Otherwise plays randomly

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: medium AI (win/block/random)"
```

---

### Task 7: Hard AI (minimax)

**Files:**
- Modify: `index.html` — add `minimax` and `aiHard`, update `aiMove`

- [ ] **Step 1: Add `minimax` and `aiHard`**

Add after `aiMedium`:

```javascript
function minimax(b, isMaximizing) {
  const result = checkWinner(b);
  if (result) return result.winner === 'O' ? 10 : -10;
  if (isDraw(b)) return 0;

  const empty = getEmptyCells(b);
  if (isMaximizing) {
    let best = -Infinity;
    for (const i of empty) {
      b[i] = 'O';
      best = Math.max(best, minimax(b, false));
      b[i] = null;
    }
    return best;
  } else {
    let best = Infinity;
    for (const i of empty) {
      b[i] = 'X';
      best = Math.min(best, minimax(b, true));
      b[i] = null;
    }
    return best;
  }
}

function aiHard(b) {
  let bestScore = -Infinity;
  let bestIndex = null;
  for (const i of getEmptyCells(b)) {
    b[i] = 'O';
    const score = minimax(b, false);
    b[i] = null;
    if (score > bestScore) {
      bestScore = score;
      bestIndex = i;
    }
  }
  return bestIndex;
}
```

- [ ] **Step 2: Update `aiMove` to call `aiHard`**

In `aiMove`, change the if/else block to:

```javascript
if (difficulty === 'easy') index = aiEasy(board);
else if (difficulty === 'medium') index = aiMedium(board);
else index = aiHard(board);
```

- [ ] **Step 3: Test minimax in browser console**

```javascript
// AI should block the imminent X win (index 2) and take a strategic position
const bTest = ['X','X',null,null,'O',null,null,null,null];
console.assert(aiHard(bTest) === 2, 'Hard AI blocks X from winning at index 2');

// On an empty board, AI should take center (index 4) — optimal first move
const bEmpty = Array(9).fill(null);
console.assert(aiHard(bEmpty) === 4, 'Hard AI takes center on empty board');

console.log('Hard AI tests passed');
```

- [ ] **Step 4: Play Hard mode — verify it is unbeatable**

Switch to Hard and play 5 games trying your best to win. Every game should end in a draw or AI win, never a player win.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: hard AI (minimax — unbeatable)"
```

---

### Task 8: Difficulty selector

**Files:**
- Modify: `index.html` — wire difficulty buttons

- [ ] **Step 1: Add difficulty button click handler**

Add after the `cells.forEach` click wiring:

```javascript
// ─── Difficulty selector ──────────────────────────────────────────────────────
document.querySelectorAll('#difficulty button').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('#difficulty button').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    difficulty = btn.dataset.level;
    resetBoard();
  });
});
```

- [ ] **Step 2: Add `resetBoard` function**

Add before the difficulty selector handler:

```javascript
function resetBoard() {
  board = Array(9).fill(null);
  gameOver = false;
  statusEl.textContent = 'Your turn';
  renderBoard();
}
```

- [ ] **Step 3: Wire "New Game" button**

Add after the difficulty selector handler:

```javascript
document.getElementById('new-game').addEventListener('click', resetBoard);
```

- [ ] **Step 4: Verify in browser**

- Click "Medium" pill → board resets, Medium becomes highlighted in red
- Click "Hard" pill → board resets, Hard becomes highlighted
- Click "New Game" → board clears, score stays the same, status returns to "Your turn"
- Play a full game, then click "New Game" — score should persist

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: difficulty selector and new-game button"
```

---

### Task 9: Full game verification + polish

**Files:**
- Modify: `index.html` — ensure initial state is correct

- [ ] **Step 1: Ensure `renderBoard()` and `renderScore()` are called on load**

Verify that at the bottom of the `<script>` block, after all event wiring, you have:

```javascript
// ─── Init ─────────────────────────────────────────────────────────────────────
renderBoard();
renderScore();
statusEl.textContent = 'Your turn';
```

- [ ] **Step 2: Full end-to-end play-through checklist**

Open `index.html` fresh (Ctrl+Shift+R to hard refresh). Verify each item:

- [ ] Page loads on Easy with empty board, score 0-0-0, status "Your turn"
- [ ] Clicking empty cell places red X with ~300ms delay before O appears
- [ ] Hovering empty cells shows blue glow; occupied cells do not glow
- [ ] Winning cells highlight yellow on game end
- [ ] Status shows correct message: "You win!", "AI wins!", "It's a draw!"
- [ ] Score increments correctly after each game
- [ ] "New Game" resets board but keeps score
- [ ] Switching difficulty resets board and keeps score
- [ ] Hard mode is unbeatable (play 3 games trying to win)
- [ ] Medium AI blocks and takes winning moves
- [ ] Easy AI plays randomly

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: complete tic tac toe game"
```

---

## Self-Review

**Spec coverage:**
- [x] Single player vs AI — Task 4 (playerMove + aiMove)
- [x] Easy / Medium / Hard difficulty — Tasks 5, 6, 7
- [x] Dark Neon theme — Task 1 (CSS)
- [x] Difficulty pill selector — Task 8
- [x] Status line with all 5 messages — Tasks 4, 5
- [x] 3×3 board, 80×80px cells, hover glow — Task 1
- [x] Score tracker — Tasks 2, 4
- [x] Win cell highlighting (yellow) — Task 4 (`endGame` + `.winner` CSS class)
- [x] New Game button — Task 8
- [x] 300ms AI delay — Task 5
- [x] Board locked after game end — Task 2 (`.locked` class)
- [x] Score persists across rounds — Task 8 (`resetBoard` does not reset `score`)

**Placeholder scan:** No TBDs, TODOs, or vague steps found.

**Type consistency:**
- `board` — `Array(9)` of `null | 'X' | 'O'` — used consistently across all tasks
- `checkWinner(b)` — returns `{ winner, line }` or `null` — used consistently in Tasks 3, 4, 7
- `isDraw(b)` — returns `boolean` — used consistently in Tasks 3, 4, 7
- `getEmptyCells(b)` — returns `number[]` — used consistently in Tasks 5, 6, 7
- `renderBoard(winLine = [])` — `winLine` is `number[]` — consistent across all render calls
- `difficulty` — string `'easy' | 'medium' | 'hard'` — set in Task 8, read in Task 5
- `resetBoard()` — defined in Task 8 before it is referenced in difficulty handler — correct order
