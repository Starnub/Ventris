# Ventris — Design Plan (draft 3)

> Working title. Idle tower defense where **you are the tower**, an abstract shape in a pitch-black void.
> It levels up for good: no prestige, no resets, no upkeep. Every piece of gear you equip shows up on the shape.

## 0. Decisions so far

| Topic | Decision |
|---|---|
| Platform | Android only. **Samsung Galaxy S25 Ultra is the only target device.** |
| Audience | Personal project. No purchases, no ads, no online features. |
| Interaction | **Menus are the gameplay.** Combat is fully automatic, with no tap abilities and no aiming. |
| Progression | New dimensions and Layers add **new multiplier types** instead of bigger numbers on the old ones. |
| Red dots | Only for actionable things, and every one clears in 2 taps or fewer. |
| Dimensions | **Finite.** 0D → 1D → 2D → 3D, with 4D possibly as a capstone (§3.4). |
| Attacks | **Each dimension has its own attack type** (§3.2). Any unlocked Form can be equipped. |
| Gear slots | **Gear slots are the parts of the shape:** Vertex, Weave (edges), Shell (faces), Cell (interior) (§4). |
| Item effects | **One trait per item,** shown on the body *and* applied to whatever attack you're using (§4.2). |
| Damage types | **Red / Green / Blue.** An enemy's color is its resistance (§5). |
| Sets | 4 pieces, one per slot. More sets, each smaller. |

---

## 1. Pillars

1. **Permanent.** Nothing ever resets.
2. **Zero upkeep.** No durability, stamina, energy, or repairs. Chores get automated or cut.
3. **You see what you wear.** Gear is fused into the shape, not bolted on, and the attack looks like the body.
4. **Lots of RNG, all of it fun.** Drops, affix rolls, rerolls, pulls. Bad luck is softened by generous pity and the Archive, never punished.
5. **Small things to finish.** Many shallow systems you can 100%, each with its own red dots and a completion moment.
6. **The menus are the game.** All decisions happen in menus, so they need to feel better than any menu you've used.
7. **Pure math visuals.** Everything is generated geometry. No art assets.

**Closest reference:** *The Tower* (Tech Tree Games), but with no runs. It's one continuous farm.

---

## 2. Core loop

```
 seconds  │ Shapes stream in → the tower auto-attacks → Flux + loot pop out
 minutes  │ Equip / roll / reforge, pull Rifts, buy Lattice nodes, clear dots
 hours    │ Push Depth, finish sets, unlock Forms, fill Codex pages
 days+    │ Ascend a dimension, perfect sets, enshrine in the Archive
```

### Depth (the farm)
- Depth is one number from 1 to ∞. Enemy HP, damage, and count grow exponentially with it.
- **Auto-Depth (default):** clear waves fast enough and you go one Depth deeper. If the void breaches your Integrity, you get pushed back up a few Depths. Nothing is lost and there's no fail screen.
- **Depth lock** lets you farm a specific Layer.
- Every **10 Depth** is a new *Layer* with its own **color theme** (§5), enemy mix, and loot table, and eventually **a new multiplier type**. Every **100** is a *Threshold* with a boss Anomaly.
- **Offline progress** pays your measured clear rate, with a generous cap. On return you get a glass "while you were gone" card that you swipe to collect.

### Where the decisions happen
- **Which Form to use** decides your attack type (§3.2). Different Layers favor different attacks.
- **Your color mix** against the Layer's enemy colors (§5).
- **Loadout presets** (Form + gear + colors), switched in one tap. Auto-Depth can switch presets by rule (e.g. "use Blue Pulse on yellow Layers").
- Gear choices, roll chasing, and set building.
- Lattice routing and Depth lock targets.

---

## 3. The player: Dimensions × Forms

### 3.1 Dimensional Ascension

| Dim | You are | Unlocks |
|---|---|---|
| **0D** | A point | Dot attack, **Vertex** slot, Flux, Bestiary. About 10 min of tutorial. |
| **1D** | A spinning line segment | Laser attack, **Weave** slot, gear drops + affix rolling |
| **2D** | A polygon | Pulse attack, **Shell** slot, polygon Forms, **Rifts** |
| **3D** | A polyhedron | Clone attack, **Cell** slot, Platonic → Archimedean Forms, **Archive** |
| **4D?** | A 4-polytope rotating through W | Capstone only (§3.4) |

Ascending takes a Threshold boss kill plus a small collection requirement. It's a big ceremony: the camera pulls back while your shape extrudes into the next dimension.

### 3.2 Attack types (one per dimension)

| | Attack | What it looks like | Best at | Geometry hook |
|---|---|---|---|---|
| **0D** | **Dot** | A simple dot with a trail | Single-target damage, crit, fire rate | A point has no size, so all the damage lands in one spot |
| **1D** | **Laser** | Pierces in a straight line, then fades | Enemies in lines, sweepers | The line has two ends, so it fires both ways as it spins |
| **2D** | **Pulse** | An outward pulse **from the player** in the polygon's shape | Crowds close to you | Number of sides matters: a triangle reaches far at its corners but leaves gaps; a hexagon covers evenly but reaches less |
| **3D** | **Clone** | A faded copy of your polyhedron appears centered on the target and hits the area several times | Bosses and tanky packs at range | **Hits = faces.** Tetrahedron hits 4 times; icosahedron hits 20 smaller times. Faces light up one by one as they hit. |

- **Any unlocked Form can be equipped**, from any dimension. Ascending adds an attack type and doesn't replace the old ones.
- Each Layer's enemy mix favors different attacks, so presets matter.
- Duals become a tradeoff in the 3D attack: cube (6 big hits) vs octahedron (8 smaller hits).

### 3.3 Forms (collectible bodies)
- **0D:** the point (just one).
- **1D:** segment variants (short/fast spin vs long/slow spin).
- **2D:** triangle → … → dodecagon, then the circle as a rare limit unlock.
- **3D:** 5 Platonic solids, then 13 Archimedean, then their Catalan duals.
- You unlock each Form once and swap freely, with no cost.

### 3.4 4D (decide at M5)
Keep it as a capstone with only the clean polytopes (5-cell, tesseract, 16-cell), or drop it. Nothing earlier depends on it. If it stays, it needs its own attack type, e.g. a **phase** attack that slides through 3-space and ignores resistances.

---

## 4. Gear

### 4.1 Slots = parts of the shape

| Slot | Part | Unlocks | Status |
|---|---|---|---|
| **Vertex** | Corners | 0D | Effects need rework (§4.3) |
| **Weave** | Edges and lines | 1D | Settled |
| **Shell** | Faces and fills | 2D | Settled |
| **Cell** | The interior volume, which holds a **fractal** | 3D | Settled |

Every item is part of the shape itself, so nothing gets bolted on top.

### 4.2 One trait, four versions
Each item has **one trait.** It shows on your body and changes whichever attack your Form uses.

**Weave (edges):**

| Item | Body | Dot | Laser | Pulse | Clone |
|---|---|---|---|---|---|
| **Dotted**: more, smaller hits | Dotted edges | Burst of 3 dots | Pulsed beam, 3 hits | Rapid segmented outline | Edges flicker, extra hits |
| **Double**: twin | Double-stroked edges | Two parallel dots | Two parallel beams | Two nested pulses | A smaller clone nested inside |
| **Braided**: wider | Twisted edge pairs | Two dots in a helix | Twisting beam, wider hit | Thicker, wavy ring | Edges twist, larger area |

**Shell (faces):**

| Item | Body | Effect on the attack |
|---|---|---|
| **Hollow** | Wireframe faces | Bigger area, less damage per hit |
| **Dense** | Solid, opaque faces | Smaller and heavier, crit-focused |
| **Mirror** | Reflective faces | Bounces: the dot ricochets, the laser reflects off its first hit, the pulse rebounds inward, the clone jumps to a second target |
| **Prism** | Rainbow-dispersing faces | Splits the attack into separate R, G and B hits (§5) |

**Cell (interior, 3D+):** a fractal lives inside the glass body. **Leveling the item adds recursion depth**, so it visibly gains detail.
- Menger sponge, Sierpiński tetrahedron, Koch snowflake slices, a Julia set cross-section, and so on.
- The effect is passive and global, e.g. "+X% damage per recursion level", "hits spawn a smaller copy of the fractal".
- Because the fractal sits inside the shape, it doesn't add visual clutter. You see it through the glass faces, and Hollow vs Dense Shell changes how visible it is, which gives a small free combo.

### 4.3 Vertex: open problem
Draft-3 ideas (truncate, round, node) don't work: **fine changes to corner geometry are unreadable on a 3D shape with 12–20 small corners.** Stellate is the exception because spikes change the silhouette.

**Rule for Vertex effects:** they must read through **silhouette, light, size, or motion**, not through fine detail.

| Candidate | Reads through | Body | Effect on the attack |
|---|---|---|---|
| **Stellate** | Silhouette | Corners pull out into spikes | Crit: spiked projectiles, the pulse's corners reach further |
| **Bead** | Size | Ball-and-stick look (big glowing orbs at corners) | Heavy impact + knockback |
| **Flare** | Light | Corners shine as star glints | A small burst at each impact point |
| **Comet** | Motion | Corners leave light trails as the shape spins (spirograph) | Attacks leave a damaging trail |
| **Beacon** | Motion | Light runs from corner to corner in sequence | Fire rate climbs while you keep attacking |

At **0D the player *is* a vertex**, so Vertex items define the whole body early on: a spiked star, a fat orb, a glinting point, a comet. That makes them a nice first slot to learn on.

### 4.4 Rarity: number sets
**Integer → Rational → Irrational → Transcendental → Imaginary → Complex**

Higher rarity means more affix lines and higher roll ceilings. Visually, **rarity changes the quality of the effect, not how many effects there are.**

### 4.5 Affixes and rolling
- 1–6 affix lines per item. Each line has a **tier (T1–T10)** and a **roll within that tier's range**.
- **Perfect line** = top tier and max roll. **Perfect item** = every line perfect, which adds a permanent shimmer.
- Sample affixes: damage %, attack rate, range, crit chance/dmg, area, extra hits, pierce, Integrity, regen, **R/G/B affinity**, **R/G/B resistance**, Flux gain, loot luck, rarity find.

### 4.6 Rerolling (the RNG sink)
| Action | Cost | Effect |
|---|---|---|
| **Reforge** | Shards | Reroll one line's value within its tier |
| **Retier** | Shards + Flux | Reroll one line's tier |
| **Transmute** | Prisms | Swap one line's type |
| **Lock** | Extra cost per lock | Protect lines during a full reroll |
| **Full reroll** | Shards | Reroll every unlocked line |

Rolls animate like a slot machine and snap into place with a haptic tick. Perfect rolls get their own sound and flash.

### 4.7 Sets (real math sets)
**Cantor Set, Julia Set, Mandelbrot Set, Borel Set, Power Set, Vitali Set**, …, plus the endgame **Empty Set**, whose bonus grows the fewer slots you fill.
- **4 pieces** (one per slot), with bonuses at 2 and 4.
- Because sets are small, there are more of them, and each one is quick to collect but slow to perfect.

### 4.8 Duplicates
A duplicate **Echoes** into the copy you own, adding a star (★1–★5). Stars raise roll ceilings and polish the effect.

---

## 5. Color: Red / Green / Blue damage types

These replace the usual physical/magic split.

- **Your attack color** comes from the R/G/B affinity on your gear. Your shape is tinted by the mix.
- **An enemy's color is its resistance.** Colors mix like light:

| Enemy color | Resists | Hit it with |
|---|---|---|
| Red | R | G or B |
| Green | G | R or B |
| Blue | B | R or G |
| Yellow (R+G) | R, G | B |
| Cyan (G+B) | G, B | R |
| Magenta (R+B) | R, B | G |
| White | everything | elites, need raw power |
| Dim gray | nothing | anything |

- You can read a wave at a glance: a yellow Layer needs a blue preset.
- **Your resistances** are affix lines, mostly on Shell. Enemies deal colored damage too.
- **Build tension:**
  - A **pure** single-color build gets a big *Purity* multiplier but gets walled by enemies of that color.
  - An even **white** build is never walled but is mediocre everywhere.
  - **Prism** Shell lets one attack hit as all three colors separately.
- The colors are **pure damage types**, with no status effects attached.

---

## 6. Pulls: Rifts

- **Prisms** come only from playing: Thresholds, milestones, Codex completions, daily local-clock bonuses. Generous.
- **What you pull:** gear, Forms.
- **Pity** is shown on screen and carries across banners: Imaginary+ guaranteed by 30 pulls, Complex by 90.
- **Banners** rotate weekly on the local clock.
- **The reveal:** a singularity collapses and then unfolds *into as many dimensions as the rarity*: point, line, plane, solid. Complex shatters the glass UI around it.
- There's x1, x10, and a skip-to-results grid.

---

## 7. Shallow completable systems

Every completion gives a **small permanent bonus**.

| System | What you complete | Reward |
|---|---|---|
| **Archive** | Enshrine gear you've outleveled. It floats in glass cases in a 3D gallery. | +tiny global stat per item (perfect ×3). Full sets unlock a pedestal plus a bigger bonus. |
| **Set Codex** | Find every piece of every set | Set-themed cosmetic |
| **Perfection Codex** | Get a perfect copy of every piece | Gold Archive pedestals |
| **Forms Codex** | Every Form per dimension | +% to that dimension's attack |
| **Bestiary** | Kill milestones per enemy shape × color (10 / 100 / 1k / 10k / 100k) | +damage vs that type |
| **Fractal Codex** | Every Cell fractal at max recursion | Global bonus |
| **Constants** *(undecided)* | Collect π, e, φ, √2, i, … as pure passive stat bonuses | Small permanent stats. They no longer change visuals or attacks. |
| **Theorems** | Achievements as "proofs" | Prisms, titles |
| **Synergy Codex** | Named item combos (§8.2) | Discovered combos stay highlighted forever |
| **Lattice** | Permanent upgrade graph (§9) | Region bonuses |

### Red dot rules
- A red dot only means there's something to do right now.
- Dots roll up the tree (tab → panel → card). Every one clears in 2 taps or fewer.
- Clearing one is physical: a glass droplet pops with a tone and a haptic tick, and the pitch goes up as you chain clears.
- **Long-press a tab** to cascade-clear its whole subtree.

---

## 8. How the player is drawn

### 8.1 Everything on the player
- **The Form**, tinted by your color mix
- **Vertex** effect on the corners
- **Weave** effect on the edges
- **Shell** effect on the faces
- **Cell** fractal inside, seen through the faces

That's everything. Each slot only touches its own part of the shape, so nothing competes for the same pixels.

### 8.2 Synergies
A short hand-made list (~20) of pairs that create a named effect, each with a Synergy Codex entry and a bonus. Examples:
- **Ellipsis** (Dotted Weave + Comet Vertex): corner trails become dotted lines of mines.
- **Hall of Mirrors** (Mirror Shell + Double Weave): twin bounces split off in opposite directions.
- **Lens** (Hollow Shell + Menger Cell): the fractal's holes focus the attack into extra pierce.

### 8.3 Inspect view
The **Form screen** shows the player large, and you can pinch-zoom and rotate it.

---

## 9. Permanent upgrades: the Lattice

- An expanding **Penrose / hex tessellation** node graph, bought with **Axioms**.
- Nodes are permanent. More of the graph opens with each dimension and Layer.
- **New multiplier types live here** (e.g. "×damage per Archive item", "×hits per face", "×Purity").
- Finishing a region gives its region bonus.

### Currencies
| Currency | Source | Spent on |
|---|---|---|
| **Flux** | Every kill | Base stats, item leveling |
| **Shards** | Salvage | Reforge / reroll |
| **Prisms** | Milestones, Thresholds, Codex | Rifts, Transmute |
| **Axioms** | Thresholds, rare drops | Lattice |

### Automation (so there's no upkeep)
- Auto-collect drops, auto-salvage by rarity/affix filters, auto-Depth, preset switching by rule, auto-claim offline progress.
- **Auto-equip is off by default.**

---

## 10. UI / UX

### Look
- **True #000** background on the OLED. The only light comes from the game.
- **Liquid glass panels with real refraction** of the live game behind them, with:
  - **chromatic dispersion** at the rims
  - **frosted blur** that varies with thickness
  - a **specular highlight that follows the gyroscope**
  - **liquid merging:** panels blend together with smooth-min SDFs
- When menus cover the game, a faint drifting field of geometry stays behind the glass so it always has something to bend.

### Feel
- **Spring physics** on everything. Every gesture can be interrupted midway.
- **Native haptics** with distinct patterns for taps, rarity reveals, perfect rolls, and red-dot clears.
- **Procedural audio** in one musical key. Kills play pentatonic notes.
- **Bottom sheets over the live battle.** You never leave the game.
- **Built for the S25 Ultra screen:** 1440×3120, ~412×891 CSS px at 3.5× DPR, 120 Hz. Edge-to-edge, with safe areas for the punch-hole camera. Main controls sit in the bottom third. Portrait.

### Main screens
| Tab | Contents |
|---|---|
| **Void** (home) | Battle, Depth, preset switch, red-dot dock |
| **Form** | Inspectable player, 4 slots, Form/Dimension swap |
| **Arsenal** | Inventory, reforge bench, filters, auto-salvage rules |
| **Rift** | Banners, pulls, pity |
| **Lattice** | Permanent upgrade graph |
| **Archive** | Gallery, Codex, Bestiary, Theorems |

---

## 11. Enemies

Every enemy is a **shape × color** combination. The shape decides how it behaves, and the color decides what it resists.
- **Swarm points** (fast, many). Best answer: Pulse.
- **Sweepers**: rotating lines. Best answer: Laser.
- **Splitting polygons** (an n-gon breaks into (n−1)-gons when killed). Best answer: Pulse or Clone.
- **Shells**: polyhedra with faces you break one at a time. Best answer: Clone (multi-hit).
- **Anomaly bosses**: Möbius strip, Klein bottle, torus knot, Lorenz attractor. Best answer: Dot or Clone.
- **Elites** roll random modifiers (shielded, splitting, hasted) and drop extra loot. White elites resist every color.

---

## 12. Tech plan

**TypeScript + WebGL2, packaged as an Android app with Capacitor.**

- **Vite + TypeScript**
- **three.js** for the scene + **custom GLSL** for glass, fields, and bloom
- **SolidJS** for UI
- **Glass layer:** DOM for layout and crisp text; a WebGL pass underneath draws all glass shapes and refracts the game through them
- **Simulation:** fixed timestep, deterministic, seeded RNG, separate from rendering. The same sim runs headless for balance scripts and offline progress.
- **Content:** items, affixes, sets, Forms, and fractals live in typed data tables
- **Save:** IndexedDB, versioned with migrations, plus export/import of a save string

### One device makes this simpler
- No low-end fallbacks. **Target: 120 fps.**
- **During development, run it as a PWA** on the phone. It updates with every push.
- **For the final build, use Capacitor.** GitHub Actions builds an APK with **native haptics**, and you sideload it.
- **Dev menu** for testing (give currency, jump Depth, force drops).

### Risks
- **Vertex readability:** handled by the silhouette/light/size/motion rule (§4.3).
- **Power growth with no prestige:** new multiplier types, balanced in log space and checked with the headless sim.
- **Menus are the whole game:** M0 proves the glass UI first.

---

## 13. Roadmap

| Milestone | Goal | Done when |
|---|---|---|
| **M0: Glass spike** | Prove the UI on the real device | Liquid-glass dock + sheet refracting an animated geometry field at 120 fps on the S25 Ultra |
| **M1: Core loop** | Point + Dot attack, enemies, Depth, Flux, save/load | Can idle-farm with auto-Depth |
| **M2: Gear** | Vertex + Weave slots, drops, affixes, reforge, auto-salvage | Items show on the body and change the attack |
| **M3: Collections** | Red-dot system, Bestiary, Archive, Codex | Clearing dots feels great |
| **M4: Dimensions 1–3** | Laser, Pulse, Clone, Shell + Cell, RGB, Rifts, Lattice | Can ascend to 3D with all four attacks |
| **M5: Depth content** | Sets, synergies, color-themed Layers, bosses | Systems complete. **Decide on 4D here.** |
| **M6: Ship to phone** | Offline progress, Capacitor APK via CI, haptics, audio, balance pass | Installed APK on the S25 Ultra |

---

## 14. Open questions
1. **Vertex effects:** which candidates from §4.3 to keep.
2. **Constants:** keep as a pure passive collection, or cut.
3. **4D:** decide at M5.
