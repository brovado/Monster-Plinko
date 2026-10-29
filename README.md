# Monster Plinko

A small, dependency-free browser prototype for an incremental idle game about an upgradeable magical plinko machine fighting monsters.

## Play it

Open [index.html](./index.html) locally, or enable GitHub Pages for this repository (Settings → Pages → deploy from the `main` branch, root folder) to host it as a page.

## Current prototype

- Automatic volleys, plus a manual **Launch volley now** button
- Balls launch upward, ricochet through the board, gain charge from rune pegs, and descend into the collection tray
- Damage resolves after the volley is collected
- Monsters grow tougher over time and award gold when defeated
- Three upgrade tracks: volley capacity, ball impact, and rune mastery
- Arcanist class framing, pause/resume, and local browser saving

## Prototype boundaries

This is an early playable feel-test, not the finished game. Progress currently saves in the same browser using local storage. Closing the page pauses the simulation; offline progress, more machine classes, branching skill trees, board layouts, and deeper effects are future work.

## Design north star

**The volley is the attack.** Individual balls acquire effects during their trip through the board, but the monster takes damage only after the whole volley lands. More balls should feel like a multi-hit build, while the Arcanist should specialize in changing what happens on the board.
