---


<!-- Slide 1: Introduction -->

<style>
h1, h2, h3 {
  text-align: center;
  font-weight: bold;
}

section {
  border: 4px solid #1e3a8a;
  padding: 50px;
  border-radius: 20px;
}
</style>

# OPEN SOURCE PROJECT:
# MINESWEEPER GAME
### Repository Link: [GitHub - unknownblueguy6/MineSweeper](https://github.com/unknownblueguy6/MineSweeper)
### Made with C++ | CLI Version

<!-- Slide 2: About the game -->
---

## 🔍 Project Overview
- A command-line Minesweeper game implemented in C++
- Designed for Unix-like systems (GNU/Linux, macOS, BSD)
- Utilizes ANSI escape codes for colored terminal output
- Built with object-oriented principles for modularity
- Includes a Makefile for easy compilation

---

## 🎯 Objectives
- Understand the implementation of a classic game using C++
- Explore the use of terminal graphics with ANSI codes
- Analyze object-oriented design in a game context
- Identify potential enhancements and extensions

---
## ★ Key Data Structures (1/2)

- **`std::vector<std::vector<Cell>>`**  
  ✅ **Why?** Represents the 2D game board grid. Provides fast access for revealing and updating cell states.

- **`struct Cell`**  
  ✅ **Why?** Encapsulates properties of each square on the board:  
  → `bool isMine`  
  → `bool isRevealed`  
  → `bool isFlagged`  
  → `int adjacentMines`  
  Helps in clear modeling of the game's logic and display.

---

## ★ Key Data Structures (2/2)

- **`std::pair<int, int>` or `Position` struct**  
  ✅ **Why?** Used to represent and pass coordinates (row, column), especially useful when scanning neighboring cells.

- **`std::queue<Position>`** *(Optional)*  
  ✅ **Why?** Used in **flood-fill logic** (BFS) to reveal safe zones without stack overflow from recursion.

- **`std::set<Position>` or `std::vector<Position>`**  
  ✅ **Why?** Keeps track of flagged cells. Useful for validating win condition or avoiding accidental reveals.

---

## 📦 Project Structure & Modeling

```plaintext
📁 MineSweeper
├── Makefile               # Build script
├── .gitignore
├── LICENSE.txt            # MIT License
├── README.md              # Project overview

├── 📁 source               # Source files
│   ├── board.hpp, board.cpp
│   ├── cell.hpp, cell.cpp
│   ├── game.hpp, game.cpp
│   ├── main.cpp
│   └── colour.hpp         # ANSI color codes

├── 📁 assets               # Demo assets (e.g., GIFs)

```
---

## 🔑 Main Source Files and Their Roles

### 1. `board.hpp` / `board.cpp`
- **Purpose**: Manages the game board, including cell states and mine placement
- **Key Functions**:
  - `initialize()`: Sets up the board with mines and numbers
  - `revealCell(x, y)`: Reveals a cell and recursively reveals adjacent cells if necessary
  - `flagCell(x, y)`: Toggles a flag on a cell

---

### 2. `cell.hpp` / `cell.cpp`
- **Purpose**: Represents individual cells on the board
- **Attributes**:
  - `isMine`: Indicates if the cell contains a mine
  - `isRevealed`: Indicates if the cell has been revealed
  - `isFlagged`: Indicates if the cell has been flagged
  - `adjacentMines`: Number of adjacent mines

---

### 3. `game.hpp` / `game.cpp`
- **Purpose**: Handles game logic and user interactions
- **Key Functions**:
  - `start()`: Begins the game loop
  - `processInput()`: Processes user commands
  - `checkWin()`: Determines if the player has won

---

### 4. `main.cpp`
- **Purpose**: Entry point of the application
- **Function**:
  - Initializes the game and starts the main loop

### 5. `colour.hpp`
- **Purpose**: Defines ANSI escape codes for colored terminal output
- **Example**:
  - `red_fg = "\033[1;31m";` for red foreground

---
## 🧠 Gameplay Mechanics

- **🎯 Objective**: Uncover all non-mine cells without triggering any mines

- **🎮 Controls**:
  - 🕹️ Move cursor: `W`, `A`, `S`, `D`
  - 🚩 Flag/Unflag a cell: `Spacebar`
  - 💣 Reveal a cell: `Enter`

- **🏁 Game End**:
  - ✅ **Win**: All non-mine cells are revealed
  - ❌ **Lose**: A mine is revealed

---

## ⚙️ Compilation and Execution

- **Prerequisites**:
  - C++11 compiler
- **Build Steps**:
  ```bash
  $ git clone https://github.com/unknownblueguy6/MineSweeper.git
  $ cd MineSweeper
  $ make
  $ ./mine

---



## ⚖️ Design Considerations

- **Command-Line Interface**:
  - Pros: Lightweight, portable, and easy to use
  - Cons: Lacks graphical interface for enhanced user experience

- **Object-Oriented Design**:
  - Enhances modularity and code maintainability

- **ANSI Escape Codes**:
  - Provides colored output for better visual cues in the terminal

- **Manual Testing**:
  - Relies on user testing; automated tests could improve reliability

---

## ❓ Frequently Asked Questions (FAQ)

---

**Q1. How are mines placed on the board?**  
**A1.** 💣 Mines are randomly placed at the start of the game using a pseudo-random number generator. The number of mines depends on the board size and difficulty level.

<br>

**Q2. How is the number displayed on each cell calculated?**  
**A2.** 🔢 When you reveal a cell, the game counts how many of the 8 surrounding cells contain mines. This number is then displayed on the cell. If it's **0**, nearby cells are auto-revealed recursively.

<br>

**Q3. What data structure is used to represent the board?**  
**A3.** 📊 The game board is stored as a **2D vector** (`std::vector<std::vector<Cell>>`), where each `Cell` contains information like `isMine`, `isRevealed`, `isFlagged`, and the number of `adjacentMines`.

---

**Q4. What happens when I flag a cell?**  
**A4.** 🚩 Flagging a cell marks it as a suspected mine. This helps you avoid revealing it by mistake and aids in strategizing your next moves. Flagged cells cannot be revealed until unflagged.

<br>

**Q5. How is game victory determined?**  
**A5.** 🏆 You win when **all non-mine cells are revealed**! The game checks this condition after every move to see if you've won.

<br>

**Q6. Can I restart or reset the game?**  
**A6.** 🔄 **Yes!** We have added a custom **Restart function** to the game. Now, you can easily restart the game without needing to relaunch the program. This feature reinitializes the board and resets all game states, allowing you to start a fresh game immediately. Just choose the restart option from the menu!

---

**Q7. Is diagonal movement allowed with WASD?**  
**A7.** ⬅️➡️ No, diagonal movement isn't supported. You can move **up**, **down**, **left**, or **right** with **W**, **A**, **S**, and **D**.

<br>

**Q8. How can I add more difficulty levels?**  
**A8.** 🎮 You can easily create **difficulty levels** like **Easy**, **Medium**, and **Hard** by adjusting the board size and mine count. Players can choose a difficulty level at the start of the game.

<br>

**Q9. Are there any cheat/debug modes?**  
**A9.** 🕵️‍♂️ Not by default! But you could add a **debug toggle** to display the mine positions during testing, making it easier to find and fix bugs.

---

**Q10. What are some future features that could be added?**  
**A10.** 🚀 Here are some cool ideas for the future:
- 🕰️ Add a **timer** to track your time
- 🏅 Implement a **leaderboard** or **player stats**
- 🎮 Build a **GUI** using libraries like **SDL**, **SFML**, or **Qt**
- 🌐 Create an **online multiplayer mode** to compete with friends

---


# 🎉 **Thank You!** 🎉

