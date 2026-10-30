# Monster Plinko — Game Design Direction

**Status:** Agreed design foundation  
**Purpose:** Record the intended game structure and development priorities before major implementation work. This document describes the target game, not a claim that these systems are already implemented.

## Core identity

Monster Plinko is an incremental RPG about operating and upgrading a magical Plinko machine to hunt monsters. The machine is the main spectacle: balls bounce through components, charges build, effects trigger, and a carefully developed machine can produce spectacular, compounding results.

The central promise:

> Build the machine. Feed it monsters. Break its limits.

The world exists to provide monsters and materials. Monsters provide the resources and challenges that let the operator build a more powerful machine.

## The campaign loop

1. **Choose an available area/map.**
2. **Search instantly** to encounter a monster from that area's population. Searching is not a timed expedition or map-traversal activity.
3. **Fight** using the Plinko machine. Ball interactions and component effects remain the centre of the experience.
4. **Harvest** monster drops: family materials, rare materials, cores, and occasional special rewards.
5. **Craft and improve** machine components, enhancements, spells, and other run equipment.
6. Repeat, unlock more dangerous areas, defeat the campaign's two minibosses, then challenge the final boss.
7. Complete the meta-game, claim permanent unlocks, and begin a fresh campaign.

## Campaign reset and meta progression

A completed meta-game resets the entire campaign. The next campaign starts fresh.

### Reset each campaign

- Operator's temporary stats, skills, and run-specific progression
- Machine layout and installed components
- Component upgrades and enhancements
- Spells and their run-specific upgrades
- Materials and crafting inventory
- Relics acquired during that campaign
- Zone, monster, and boss progress

### Persist between campaigns

- Unlocked operators/classes
- Difficulty unlocks, tracked separately for each operator
- Unlocked maps and campaign options
- Relic discoveries/unlocks
- Recipe and content unlocks intended as meta progression
- Campaign achievements and milestones

Permanent progression should primarily expand choices and possibilities, rather than simply inflate starting stats until earlier content becomes irrelevant.

## Monster families and loot

There are **five primary monster families**, each associated with one machine component. Each family is a targeted farming source for a corresponding family-specific material. The exact family names, component assignments, material names, and combat identities are to be designed in the monster/loot phase.

Families should be mechanically meaningful, not merely visual skins. Their creatures can interact with, disrupt, or reward particular machine mechanics. Each family can contain common creatures, variants, elites, and a family miniboss or other notable encounter.

There are also **story-level monster forces/families** that connect the five primary families and lead into the campaign's central conflict. These are not required to map one-to-one to machine components.

### Loot principles

- Every ordinary monster should contribute something useful to machine progression.
- The five family materials are the primary targeted farming resources.
- Rare drops, cores, and special rewards provide excitement and meaningful milestones.
- Components should generally be crafted through understandable recipes, not bought from a conventional generic parts shop.
- Random drops can provide rare variants, special enhancements, or exciting shortcuts, but players should usually know which monsters to hunt for a desired resource.
- Avoid loot that accumulates without a clear use in building or improving the machine.

## Workshop, inventory, and crafting

The conventional buy-parts shop is intended to be removed or fundamentally replaced.

The workshop becomes an operator's crafting and machine-development space. Its inventory should distinguish between:

- **Components:** Physical machine pieces installed on the board.
- **Enhancements:** Improvements to components.
- **Spells:** Abilities assigned to components.
- **Materials:** Resources harvested from monsters and used in recipes.
- **Relics:** Rare effects that fundamentally modify game rules.

The crafting system should connect monster farming directly to machine development. Recipes, upgrade costs, component tiers, and material sinks will be designed together so every family remains relevant.

### Meta profile, operation slots, and campaign selection

Operator and difficulty selection belongs to the main-menu meta layer, not the in-operation Character screen.

- The main menu is the campaign command hub. It supports resuming a save, loading a slot, starting a new operation, saving the active slot, and importing/exporting a portable backup.
- Three independent operation save slots are available. Each slot stores its own operator, difficulty, character progression, machine, inventory, relics, and campaign state. Gameplay autosaves to the active slot; the explicit save action also downloads a JSON backup.
- Starting a new operation requires selecting a destination slot, an unlocked operator, and a difficulty unlocked for that operator. Replacing a populated slot requires confirmation.
- A separate permanent meta profile stores operator unlocks, each operator's difficulty ladder, and campaign completion records. It is not reset when a new operation begins.
- Existing single-save browser data migrates into Slot 1. Existing operator/difficulty choices are retained and registered as unlocked for that legacy operation.
- Engineer is initially available with Story and Standard. Scavenger unlocks by defeating the Dune Warden; Gambler unlocks by defeating the Hollow Colossus; Guardian unlocks by completing the campaign. Newly unlocked operators begin with Story difficulty.
- Difficulty unlocks are tracked independently for each operator: completing Story unlocks Standard; completing Standard unlocks Veteran; completing Veteran unlocks Nightmare. The final boss must be defeated to record a campaign completion and advance this ladder.
- The Character screen is now limited to in-operation attributes and derived statistics. Operator and difficulty cannot be changed from inside a running operation.
- The relic discovery archive remains separately persisted and is not tied to an individual operation slot.

The four operator perks and difficulty multipliers remain prototype balance values as described below.

### Campaign and zone progression prototype

The campaign now has five selectable hunting areas across three tiers. Areas use instant monster selection; there is no travel timer or map traversal. The Plinko machine remains the combat loop.

| Tier | Area | Unlock |
|---|---|---|
| I | First Forest | Available at campaign start |
| I | Glasswind Desert | Defeat 15 creatures in First Forest |
| II | Ironroot Mountain | Defeat the Dune Warden miniboss in Glasswind Desert |
| II | Hollowdeep Cave | Defeat 15 creatures in Ironroot Mountain |
| III | The Ashen Reach | Defeat the Hollow Colossus miniboss in Hollowdeep Cave |

- Each area has its own four-monster population, with family-linked material drops retained.
- The Dune Warden (260 HP) and Hollow Colossus (620 HP) are selectable miniboss encounters. Defeating each permanently unlocks the next tier's first area.
- The Ashen Reach contains four minion types. Defeat 20 Ashen Reach minions to reveal the Ashen Sovereign (1,800 HP), the campaign's final encounter.
- Campaign area kill counts, defeated miniboss IDs, and completion status are stored in the regular run save and included in account exports.
- Bosses use a dedicated encounter-pressure loop rather than ordinary family specials. Spring impacts charge separate Machine and Operator threat tracks; each resolves after the player's volley when full.
- The Dune Warden's Machine Breaker resets one component charge bank and its Operator strike deals 2 HP. The Hollow Colossus uses the same dual-threat structure with a 3 HP operator strike.
- The Ashen Sovereign has two phases. Crossing 50% HP triggers Phase II, clears both pressure tracks, and increases their charge rate by 45%. Phase II's machine attack resets two component charge banks; its operator strike deals 4 HP, with a 2 HP fallback pressure hit when neither bar is full.
- Boss HP uses a separate difficulty curve (Story 0.72×, Standard 1×, Veteran 1.35×, Nightmare 1.8×). Boss gold rewards use a separate multiplier (1.15×, 1.5×, 2×, 2.75× respectively).
- These are first-pass tuning values and need playtesting against low-, mid-, and high-synergy machine builds.

### Implemented prototype foundation

- The five craftable core components are tied to their family materials: Bumper / Bulwark Plates, Peg / Burrow Tubes, Gate / Thread Silk, Booster / Gale Sacs, and Target / Verdant Cores.
- Base fabrication currently costs 2 family materials plus a modest gold fee (Gate costs 1 Thread Silk).
- Installed components can be refined from Tier I to Tier III. Each tier adds 15% component-ability damage.
- Tier II costs 4 matching family materials and 45 gold; Tier III costs 8 matching family materials and 110 gold.
- Tier II requires the first component-tree node; Tier III requires the second. This makes component specialization part of the refinement path.
- Component-tree nodes and spell upgrades remain separate progression tracks. Their existing node effects, spell unlocks, and spell ranks complement physical component tiers.
- Refinement applies to the five craftable core components. Fixed board hazards are not refinable.
- These values are prototype balance values and should be revisited during campaign progression and difficulty balancing.

## Relics

Relics are scarce, powerful, run-specific modifiers. They should alter how the machine behaves and create new build identities, rather than functioning as ordinary stat upgrades.

Example concepts (illustrative, not final balance):
- A Target can generate an additional ball when its charge reaches maximum.
- After a Bumper charge activates, bumper hits restore operator health for a short duration.
- Booster activations can build stacking momentum during a volley.
- Gate activations can occasionally duplicate a ball.

Relics may be awarded for major quests, achievements, minibosses, bosses, or other exceptional milestones. A limited number of equipped relics is worth considering to preserve meaningful choices. The relic collection/discovery system can persist between campaigns, while relics equipped during a campaign reset with that campaign.

### Implemented prototype foundation

- Five relics are implemented, each tied to a machine interaction:
  - **Starfall Lens (Target):** Target ability activations queue one extra ball for the next volley.
  - **Heartwood Core (Bumper):** After a Bumper ability activates, the next three Bumper hits each restore 1 operator HP.
  - **Stormglass Flywheel (Booster):** Booster activations build up to five momentum stacks per volley, adding 5% damage per stack to the triggering ball and extending its boost.
  - **Mirror Gate (Gate):** Gate ability activations have a 20% chance to queue an extra ball for the next volley.
  - **Prospector’s Knot (Peg):** Peg ability activations have a 25% chance to harvest one additional material from the current monster family.
- Ordinary monster kills have a 3.5% relic discovery chance. A pity counter guarantees a discovery after 25 kills without one. A relic already found in the current run cannot drop again.
- Up to three discovered run relics can be equipped at once. The Relics inventory tab shows each relic's effect and whether it is equipped, held in the current run, previously discovered, or undiscovered.
- The discovery archive is stored separately in the browser so it survives reloads and a fresh account reset. Relics held and equipped for combat remain part of the saved run state.
- Relic drops and effects are prototype foundations. Boss/quest reward tables, a proper campaign reset, and balance tuning remain future work.

## Campaign world and progression

Each campaign has three zone tiers, with multiple map choices in the first two tiers.

### Tier 1 — Frontier
- Forest
- Desert

### Tier 2 — Deep Wilds
- Mountain
- Cave

### Tier 3 — Boss territory
- A dedicated final-region map containing the boss's minions.
- The player defeats a required number of minions to draw out/unlock the final boss.

Maps within a tier should offer different monster populations, material opportunities, and farming decisions—not merely different scenery.

The campaign contains:
1. A Tier 1 miniboss that tests whether the player has established a functional machine.
2. A Tier 2 miniboss that tests whether the player has developed meaningful synergies.
3. A Tier 3 final boss, unlocked after enough of its minions have been defeated.

## Boss design

The final boss is intended to be genuinely difficult and should demand a well-developed, high-synergy machine. It should not be balanced merely by giving it an enormous health pool.

The final encounter has **two phases**:
- **Phase 1:** Hard but manageable, giving the player room to operate and build momentum.
- **Phase 2:** A dramatic escalation—the “oh no, I may not survive this” phase—with significantly greater pressure.

The boss can have multiple independent charge bars. Each bar represents a distinct threat or mechanic, such as:
- Disabling or disrupting a machine component
- Damaging or weakening the operator
- Interfering with ball movement, charges, or machine operation

Charge bars should force build and survival decisions. A high-damage machine that neglects every defensive or utility option should be vulnerable. The boss should punish incomplete builds, not merely low stats.

The encounter should be the examination of the machine the player has built. Defeating it should feel like a payoff for the campaign's progression and synergies.

## Operators and difficulty

The meta-game includes operator/class selection and difficulty selection.

- Operators have distinct starting advantages and build tendencies, but should not lock the player into one rigid build.
- Difficulty unlocks are tracked per operator.
- Higher difficulties should introduce meaningful changes: enemy abilities, encounter modifiers, elite variants, material/drop adjustments, or other new pressures—not only inflated monster health.
- Maps and other campaign options may unlock through meta progression and operator-specific accomplishments.

Possible operator identities (examples only): Engineer (component crafting/upgrades), Arcanist (spell effects), Artificer (material yield and specialization), Juggernaut (survival), Gambler (critical/random effects).

## Progression cadence

The game should offer overlapping goals at several timescales:

| Timescale | Desired reward |
|---|---|
| Seconds | Satisfying ball interactions and component triggers |
| Minutes | Monster kills, drops, and visible machine upgrades |
| 15–30 minutes | Recipes, variants, and area unlocks |
| 1–2 hours | Major upgrades, relics, and minibosses |
| Several hours | Final-boss preparation and high-synergy builds |
| Campaign completion | Permanent unlocks and a fresh campaign with new possibilities |

## Development priorities

Build the connective systems in this order:

1. **Monster families and loot** — define the five component-linked families, their material drops, combat identities, and story-level connections.
2. **Inventory and crafting workshop** — replace conventional part purchasing with a coherent RPG inventory and crafting flow.
3. **Component recipes and upgrades** — connect family materials to component creation, enhancement, and progression.
4. **Relic system** — implement rare, transformative, run-specific modifiers and their unlock/discovery rules.
5. **Campaign and zone progression** — implement three tiers, map choices, monster pools, miniboss gates, and final-zone minion threshold.
6. **Operator classes and difficulty unlocks** — implement fresh campaign selection and operator-specific meta progression.
7. **Boss encounters and balancing** — implement the two minibosses, two-phase final boss, multiple charge mechanics, and tune the campaign around the final challenge.

## Design guardrails

- Keep the Plinko machine and its live combat as the main event.
- Monster search is instant; do not turn the game into a map-traversal or timed-expedition game.
- Preserve the incremental satisfaction of steadily improving a build and then reaching spectacular, compounding interactions.
- Make monster drops feed machine upgrades; avoid disconnected currencies and loot.
- Make choices and synergies matter. Avoid relying on bigger numbers as the only form of progression.
- The final boss is the campaign's destination. Endless play may exist as an optional post-campaign mode, not the primary campaign objective.
- This document is a target design. Existing prototype code may not yet implement these systems.
