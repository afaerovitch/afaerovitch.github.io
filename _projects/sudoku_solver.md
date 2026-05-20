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
- **Other Tools:** Maven

### Algorithm

The solver utilizes `Depth-First Search (DFS)` to iterate through different board states until a solution is found. To reduce the search space, I introduced a `constraint validation` function to eliminate impossible states as soon as they were found, such as the same digit appearing twice in a single row. I call this implementation the "naive" algorithm because it is the common approach for quickly solving standard Sudoku puzzles.

After this, I implemented `domain pruning`, followed by a `Minimum Remaining Values (MRV)` heuristic. After implementing this search, I saw my first major increase in performance. I also tested the `Least Constraining Value (LCV)` heuristic but saw no major benefit to doing so.  The overhead calculations for finding the least constraining value were more time intensive than just exploring the search space. I believe this is due to the domain of values already being limited with domain pruning.

With this new baseline, I looked at further improving the algorithm with a variation of the `AC-3 arc consistency` algorithm. The only modification I made was including an attribute to constraint arcs that defined which constraint rule to apply. I applied this algorithm to ensure constraint propagation and prevent checking cells that were unaffected by the changes in the board state.

Even though AC-3 improved my performance, it was minimal due to some suboptimal processes in my implementation. To optimize the algorithm, I began `caching` reoccurring calculations, `mapping explored states` to the cache, and implementing `local constraint validation` (before this, AC-3 was performing a board-wide constraint validation function after every propagation step). Localizing validations proved to be the most significant improvement, while the others only gave marginal benefits. Using a `hash map` for the explored states only saw a benefit on some puzzles, as shown in the results.

## Results & Performance

These result photos are taken directly from my project presentation in the AI course. They show the solve times of *NaiveDFS* (my first algorithm), *MrvAc3Dfs* (MRV heuristic with AC-3 constraint propagation), *MrvLcvAc3Hash* (MRV + LCV, AC3 propagation, and explored state mapping), and *MrvAc3Hash* (MrvAc3Dfs with explored state mapping). All experiments were run on my MacBook Air.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sudoku_solver/NewYearsFirework.JPG" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sudoku_solver/MediumKropki.JPG" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sudoku_solver/RenbanKiller2.JPG" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## Future Improvements

- [ ] Stricter constraint validation + Constraint-rule library
- [ ] Uniqueness Checking
- [ ] Setting New Puzzles
