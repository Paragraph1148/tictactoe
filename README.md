## Tic‑Tac‑Toe React App

A simple, browser‑based Tic‑Tac‑Toe game built with **React** and functional components.  
The code is split into three files:

| File                     | Purpose                                                        |
| ------------------------ | -------------------------------------------------------------- |
| `App.js`                 | Main game logic, board state, win/tie detection, turn handling |
| `components/Square.js`   | Individual square component                                    |
| `components/Patterns.js` | Winning patterns (rows, columns, diagonals)                    |

### Features

- Two‑player play (X vs O) on a 3×3 grid
- Automatic win detection using predefined patterns
- Tie detection when all squares are filled
- Game resets automatically after a win or tie (via an alert)

---

## Getting Started

### Prerequisites

- **Node.js** (v14 or newer)
- **npm** or **yarn**

### Installation

```bash
# Clone the repository
git clone https://github.com/your‑username/tic-tac-toe-react.git
cd tic-tac-toe-react

# Install dependencies
npm install   # or: yarn install
```

### Running the App

```bash
npm start   # or: yarn start
```

The development server will launch at `http://localhost:3000`. Open that URL in a browser to play.

---

## Project Structure

```
tic-tac-toe-react/
├─ src/
│  ├─ App.js               # main component, state management
│  ├─ App.css              # styling for board & squares
│  └─ components/
│     ├─ Square.js         # clickable square UI
│     └─ Patterns.js       # export const Patterns = [...]
├─ public/
│  └─ index.html
├─ package.json
└─ README.md               # (this file)
```

### Key Code Walk‑through

#### 1. State Management (`App.js`)

```js
const [board, setBoard] = useState(Array(9).fill(""));
const [player, setPlayer] = useState("O");
const [result, setResult] = useState({ winner: "none", state: "none" });
```

- `board` holds the 9 squares.
- `player` toggles between `"X"` and `"O"` after each move.
- `result` records the outcome (winner or tie).

#### 2. Turn Switching

```js
useEffect(() => {
  checkWin();
  checkIfTie();

  // Switch player after every board update
  setPlayer((prev) => (prev === "X" ? "O" : "X"));
}, [board]);
```

The effect runs whenever the board changes, checks for a win/tie, then flips the active player.

#### 3. Win Detection (`checkWin`)

```js
Patterns.forEach((pattern) => {
  const first = board[pattern[0]];
  if (!first) return; // empty square → cannot win
  const win = pattern.every((idx) => board[idx] === first);
  if (win) setResult({ winner: player, state: "won" });
});
```

Iterates over each winning pattern; if all three indices contain the same non‑empty symbol, the current player wins.

#### 4. Tie Detection (`checkIfTie`)

```js
if (board.every((square) => square !== "")) {
  setResult({ winner: "No One", state: "Tie" });
}
```

When every square is filled and no win was found, the game ends in a tie.

#### 5. Square Component (`Square.js`)

```js
function Square({ val, chooseSquare }) {
  return (
    <div className="square" onClick={chooseSquare}>
      {val}
    </div>
  );
}
```

A simple `div` that displays the square’s value and calls `chooseSquare` when clicked.

---

## Styling (App.css)

```css
.App {
  text-align: center;
}
.board {
  display: inline-block;
  margin-top: 2rem;
}
.row {
  display: flex;
}
.square {
  width: 80px;
  height: 80px;
  border: 2px solid #333;
  font-size: 2rem;
  line-height: 80px;
  cursor: pointer;
}
```

Feel free to customize colors, sizes, or add animations.

---

## Extending the Project (Study Ideas)

| Idea                         | What You’ll Learn                           |
| ---------------------------- | ------------------------------------------- |
| **Add a score board**        | State lifting, persisting data across games |
| **Implement AI opponent**    | Minimax algorithm, deeper React logic       |
| **Responsive design**        | CSS Grid/Flexbox, media queries             |
| **Write unit tests**         | Jest + React Testing Library basics         |
| **Deploy to Netlify/Vercel** | CI/CD pipelines, static site hosting        |

Pick one that excites you and try it out—hands‑on experimentation is the fastest way to solidify concepts!

---

## License

This project is licensed under the **MIT License**. See the `LICENSE` file for details.
