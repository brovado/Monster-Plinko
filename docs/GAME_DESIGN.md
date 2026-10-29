# Monster Plinko — Game Design

## Core fantasy
Build an increasingly powerful magical machine that automatically attacks monsters. The satisfying part is watching a volley behave differently as upgrades and board effects grow more elaborate.

## Core loop
1. The machine launches a volley of balls upward.
2. Balls travel through a fixed board and ricochet off pegs and special components.
3. Collisions can add persistent effects to individual balls.
4. Every ball lands in the collection tray.
5. The tray resolves the combined volley damage against the current monster.
6. Defeating the monster awards gold and advances to the next round.
7. Spend gold on upgrades; the machine repeats automatically.

The volley is one attack, not a sequence of separate monster hits. The monster should not lose health until the volley has been collected and resolved.

## Starter machine: Arcanist
The Arcanist is a board-modification class. Its identity is enchanting the route rather than simply adding raw damage. Rune pegs charge balls; later abilities could add lightning chains, portals, gravity wells, and temporary board-wide enchantments.

Possible future branches:
- **Storm Weaver:** charge collisions, chain lightning, burst damage.
- **Gravity Sage:** pull balls toward selected pegs, bend trajectories, extend routes to trade time for stronger effects.

## Other future machine identities
- **Artillerist:** more balls, heavy balls, critical hits, slower high-impact shots.
- **Alchemist:** poison, explosions, splitting balls, and combo reactions.

## Progression principles
- More bounces should not automatically mean free extra damage; long routes need a trade-off or a build investment.
- Multi-ball should create a recognizable multi-attack identity.
- Upgrades should be legible: each should clearly change either the volley, ball behavior, or board.
- Keep the board layout recognizable. Unlock alternate layouts later rather than requiring players to build every peg themselves.
- Prefer a small number of meaningful synergies over a huge list of tiny percentage upgrades.

## Prototype scope
The first playable slice should prove:
- automatic and manual volley launch
- upward launch and downward peg traversal
- persistent per-ball rune charge
- tray-based volley resolution
- monster health, defeat, gold reward, and next round
- at least one upgrade that increases balls per volley

## Open questions for later
- Should balls have individual types, or should upgrades modify a common ball?
- Can effects slightly weaken a ball as well as empower it?
- Should alternate board layouts be unlocked by class, milestone, or prestige?
- What is the reset/prestige fantasy once monster scaling gets large?
