---
layout: page
title: Sudoku Solver
description: Experimenting with different AI algorithms to solve variant Sudoku puzzles
img: /assets/img/sudoku_solver/gw_board.png
importance: 1
category: School
featured: true
---

## Overview

`Variant Sudoku` describes a class of puzzles that riff on the traditional Japanese puzzle game. These puzzles add new constraints on top of the standard 1-9 in every row, column, and box (for example, the Anti-Knight constraint prevents the same digit from appearing one chess knight's move away from itself). For the final project in my AI course, I developed an algorithm that could efficiently solve many of these different rulesets.

### Technology Stack

- **Language:** Java
- **Key Libraries:** Maven
- **Other Technologies:** Any other relevant tech

### Algorithm

The solver utilizes `Depth-First Search (DFS)` to iterate through different board states until a solution is found. To reduce the search space, I introduced a `constraint validation` function to eliminate already impossible states, such as the same digit appearing twice in a row. I call this implementation the "naive" algorithm because it is the common approach for quickly solving standard Sudoku puzzles.

After this, I implemented `domain pruning`, followed by a `Minimum Remaining Values (MRV)` heuristic. (WIP)

## Results & Performance

(WIP)

## Future Improvements

- [ ] Stricter constraint validation + Constraint-rule library
- [ ] Uniqueness Checking
- [ ] Setting New Puzzles
