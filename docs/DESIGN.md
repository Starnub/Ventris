# Ventris — Design Plan (draft 8)

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
| Stacking | **Within a slot, every trait uses a different visual axis, so traits can run at the same time.** Vertex: Flare + Comet + Beacon. Weave: Dotted + Double + Wavy. A late unlock (Harmonics) enables it, and it adds no extra combo effects (§4.3). |
| Constants | **Relics that change how you play.** One equipped at a time, each one big (§6). |
| Scope | **A "forever game."** Development continues for as long as it's fun, so there's no feature cap. |
| Feature types | **Modular** (fully independent, can be switched off) and **integrated** (depends on or feeds other features), kept roughly balanced (§16). |

---

## Glossary (quick memory aid)

| Term | Meaning |
|---|---|
| **Depth** | How deep into the void you're farming. One number, keeps going up. |
| **Layer** | Every 10 Depth: a new zone with its own enemy mix and color theme |
| **Threshold** | Every 100 Depth: a boss fight. Bosses guard Constants (confirmed). |
| **Form** | Your body's shape (point, line, polygon, polyhedron). It decides your attack. |
| **Dot / Laser / Pulse / Clone** | The four attacks: 0D, 1D, 2D, 3D |
| **Vertex / Weave / Shell / Cell** | The four gear slots: corners, edges, faces, interior |
| **Plate** | A face acting as a shield on that side of you. Breaks and regrows. |
| **Integrity** | Your HP. Breaching it pushes you back up a few Depths; you never lose anything. |
| **Trait** | The one visual + attack effect an item has (e.g. Dotted, Comet) |
| **Harmonics** | Late unlock that lets a slot run 2–3 traits at once |
| **Constant** | A relic that rewrites a combat rule (π, e, i, 1, 0) |
| **Euler's Identity** | Owning e, i, π, 1 and 0 unlocks a 2nd Constant slot |
| **R / G / B** | Damage types. An enemy's color is what it resists. |
| **Lattice** | The permanent upgrade tree: a big glowing node graph bought with Axioms |
| **Archive** | A gallery where outgrown gear goes on display for a small permanent bonus |
| **Rift** | Pulls (gacha) using Prisms |
| **Flux / Shards / Prisms / Axioms** | Currencies: kills / salvage / pulls / Lattice |

---

## 1. Pillars

1. **Permanent.** Nothing ever resets.
2. **Zero upkeep.** No durability, stamina, energy, or repairs. Chores get automated or cut.
3. **You see what you wear.** Gear is fused into the shape, not bolted on, and the attack looks like the body.
4. **Lots of RNG, all of it fun.** Drops, affix rolls, rerolls, pulls. Bad luck is softened by generous pity and the Archive, never punished.
5. **Small things to finish.** Many shallow systems you can 100%, each with its own red dots and a completion moment.
6. **The menus are the game.** All decisions happen in menus, so they need to feel better than any menu you've used.
7. **Pure math visuals.** Everything is generated geometry. No art assets.
8. **Forever game.** Built to keep growing. Every new feature plugs into the same structure and either stands alone or connects on purpose (§16).

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
| **Vertex** | Corners | 0D | Settled |
| **Weave** | Edges and lines | 1D | Settled |
| **Shell** | Faces and fills | 2D | Settled |
| **Cell** | The interior volume, which holds a **fractal** | 3D | Settled |

Every item is part of the shape itself, so nothing gets bolted on top.

### 4.2 One trait, four versions
Each item has **one trait.** It shows on your body and changes whichever attack your Form uses.

**Weave (edges):** each trait uses its own visual axis. Dotted is the **pattern**, Double is the **count**, Wavy is the **shape**. Any combination stays readable: two parallel dotted sine waves is still obviously all three.


| Item | Body | Dot | Laser | Pulse | Clone |
|---|---|---|---|---|---|
| **Dotted**: more, smaller hits | Dotted edges | Burst of 3 dots | Pulsed beam, 3 hits | Rapid segmented outline | Edges flicker, extra hits |
| **Double**: twin | Double-stroked edges | Two parallel dots | Two parallel beams | Two nested pulses | A smaller clone nested inside |
| **Wavy**: wider sweep | Edges ripple as sine waves | The dot snakes along a sine path | The beam oscillates side to side, covering a wider band | The ring's edge ripples outward | Clone edges ripple, larger area |

**Shell (faces) = defense.** Vertex and Weave shape your attack. Shell shapes **how you take hits.**

**Base rule: faces are shield plates.** Each face blocks hits coming from its side. When enough damage gets through, the plate breaks and only then does damage reach your Integrity (your HP). Broken plates regrow on their own (no upkeep). Your Form changes how this plays: a tetrahedron has 4 big plates, an icosahedron has 20 small ones.

**Traits** *(proposed)*. Faces are clear glass by default. Each trait changes a different property of the glass, so all three can stack (Harmonics).

| Trait | Property | Body | Effect |
|---|---|---|---|
| **Exploded** | Position | Faces float out from the body with **visible gaps** between them | **Trades defense for attack.** Hits can slip through the gaps straight to Integrity. Your attacks pass through the floating faces as **lenses** and focus to a bright, visible focal point that hits hard. |
| **Absorb** *(proposed)* | Brightness | Faces fill with light as they take hits: dark means empty, bright means full | Plates **soak up hits as light** instead of cracking. When a plate is full it **flashes**, hitting everything near that side, then goes dark and starts filling again. How bright a face is tells you how close it is to flashing. |
| **Stained** | Color | Faces gradually become stained glass | Each plate **takes on the color of the last thing that hit it** and resists that color from then on. You can see which side gets hit by what. |

All three together: stained-glass lenses floating around you, each glowing brighter as it fills. Interplay happens without extra rules: Exploded plates sit further out, so Absorb's flash goes off further from your body. **Stained lenses do not tint attacks** (decided).

Dropped: **Crackle** (crack lines get too busy on 12–20 faces), **Heartbeat** (rhythmic shove), **Phase** (fade-in/out dodge), **Mirror** (an opaque, reflective finish can't double as a see-through lens), Hollow (hides other face traits), Dense (hides the Cell fractal), Prism (attack-only).

**Cell (interior, 3D+):** a fractal lives inside the glass body. **Leveling the item adds recursion depth**, so it visibly gains detail.
- Menger sponge, Sierpiński tetrahedron, Koch snowflake slices, a Julia set cross-section, and so on.
- The effect is passive and global, e.g. "+X% damage per recursion level", "hits spawn a smaller copy of the fractal".
- Because the fractal sits inside the shape, it doesn't add visual clutter. You see it through the glass faces.

### 4.3 Vertex: light and motion
Corners are tiny on a 3D shape with 12–20 of them, so fine changes to their geometry can't be read. **Vertex effects show through light and motion instead.** That rule holds up at any size.

| Item | Body | Effect on the attack |
|---|---|---|
| **Flare** | Corners shine as star glints | A small burst at each impact point |
| **Comet** | Corners leave light trails as the shape spins (spirograph) | Attacks leave a damaging trail |
| **Beacon** | Light runs from corner to corner in sequence | Fire rate climbs while you keep attacking |

At **0D the player *is* a vertex**, so these define the whole body early on: a glinting point, a comet, a pulsing beacon.

New Vertex traits can be added later as long as they read through light or motion.

#### Harmonics (integrated, late unlock)
The three Vertex traits don't conflict: a corner can glint, leave a trail, and pass light to the next corner **all at the same time.** Harmonics simply lets them run together.
- The slot starts with **1 socket**. The *Harmonics* track (fed by item stars and a Lattice region) unlocks a **2nd and 3rd socket**.
- Each extra socket holds the trait of another item you own for that slot. Only the main item's affixes count.
- **No combo effects.** Each trait does exactly what it does alone, and all three just run together.
- **Weave gets the same treatment** (Dotted, Double, and Wavy use separate axes). **Shell gets it too:** Exploded, Crackle, and Stained use separate properties (§4.2).

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
  - **Stained** Shell plates pick up resistance to whatever color keeps hitting them.
- The colors are **pure damage types**, with no status effects attached.

---

## 6. Constants (relics)

Constants are **rare relics that change the way you play.** They aren't stat sticks: each one rewrites a rule of combat in a way you can **see**, and it's tied to what the number actually means.

**The bar:** a Constant has to change a *rule of the world* (how attacks move, how enemies move, what you are, how enemies relate to each other). If it can be described as "+X% under condition Y", it isn't a Constant.

### 6.1 Rules
- **One equipped at a time.** A second slot is unlocked by *Euler's Identity* (§6.3).
- **Where they come from:** each Constant has a home **Threshold boss**. The first kill guarantees it.
- **Leveling reveals digits.** π goes 3 → 3.1 → 3.14 → 3.141 → 3.1415, and e goes 2 → 2.7 → 2.71 → … Re-killing its boss with Depth lock drops the next digit. Constants without useful digits get their own ladder (i: i → i² → i³ → i⁴).
- Every Constant works with all four attack types.

### 6.2 Euler's five

| Constant | Meaning | Rule change | Dot / Laser / Pulse / Clone | Downside |
|---|---|---|---|---|
| **π** (Orbit) | The circle | Attacks don't fly outward. They **circle you** at your range radius. | Dots orbit / the beam sweeps a full circle like a lighthouse / pulse rings spin and linger / clones orbit you | Nothing beyond your radius gets hit |
| **0** (Null) | Nothing | **You stop attacking.** Your shape grows and erases whatever touches it, scaling with Integrity. | Attack replaced by contact | No range at all |
| **e** (Growth) | Exponential growth | Attacks **start tiny and grow exponentially** as they travel. Far enemies take huge hits, close ones take tiny hits. | The dot swells into an orb / the beam widens into a cone / the pulse gets *stronger* as it expands / the clone starts small and swells | Weak up close |
| **i** (Imaginary) | i · i = −1: two imaginaries make a real | **The first hit deals nothing and turns the enemy into a translucent ghost** (it's now imaginary). **The second hit makes it real again** and deals the pair's damage *squared* (see §6.5). | Dot: steady ghost/shatter rhythm / Laser: one pass ghosts a whole line, the next shatters it / Pulse: two-beat rings, ghost then shatter / Clone: hits several times, so it does both in one attack | Every enemy needs at least two hits, so swarms of weak enemies take longer |
| **1** (Unity) | Identity: one whole | **All enemies in a wave share one health pool.** Damage to any of them hurts all of them. Thin lines link them into one constellation. | Area attacks hit the pool once per enemy touched, so AoE becomes king | Nobody dies until the whole wave does, so they all keep advancing |

### 6.3 Euler's Identity
**e^(iπ) + 1 = 0** uses exactly these five. Collect all five and *Euler's Identity* unlocks the **second Constant slot**, and the equation fills in on screen as you go. With two slots, combinations happen naturally with no special effects needed: **1 + i** sends every squared shatter into the shared health pool. **e + i** has the second hit land harder at range, so distant shatters are enormous. **e + π** gives orbits that grow as they circle.

### 6.5 Balancing i
**Never square raw damage.** Late-game hits are around 10¹², and squaring that gives 10²⁴, which breaks every number in the game. Square the hit *relative to the current Depth* instead:

```
S     = reference enemy HP at the current Depth
pair  = d₁ + d₂                    (each hit after resistances)
dealt = k · S · (pair / S)²
```

- **Grows faster than normal damage, but stays bounded.** What gets squared is your power *relative to where you are*, not the raw number. A pair worth 1× an enemy's HP deals k×. Worth 2×, it deals 4k×. Worth ½×, it deals k/4×.
- **Auto-Depth keeps it in check.** Any lead i gives you pushes you deeper, which raises S and pulls the ratio back down. The game corrects itself.
- **One tuning knob:** k. The digit ladder (i → i² → i³ → i⁴) raises k a step at a time.
- **Where it shines:** tanky targets (bosses, Shells) and multi-hit attacks. **Where it's weak:** swarms of enemies that would otherwise die in one hit.
- **Ghosts stay ghosts** until hit again. No timer, which would be a form of upkeep.
- **Ghosts can still hurt you** (decided). It keeps i a pure offense relic with a real cost.
- **Check it with the headless sim** (§13) before shipping: equilibrium Depth with i vs without, and clear times against swarm vs boss Layers.

### 6.4 Rejected ideas
Kept here so they don't get proposed again: φ (Fibonacci hit scaling), γ (harmonic screen-wide hits), √2 (branching splits), δ (stat reroll chaos), −1 (color inversion), ∞ (wrapping projectiles), old e (damage grows while unhit), old i (phantom waves; 4-fold attack copies), old 1 (merge into one big strike), golden angle (sunflower planting), 2 (binary split), ℵ₀ (re-fire on kill), ε (micro-hit dust), i as Quarter Turn (velocity rotation), i as rotating battlefield (**rotation in general doesn't fit i**), i as Interference (not chosen; Imaginary won).

---|---|
| **Golden angle** (137.5°, from φ) | Attacks stop targeting. They're **planted** at golden-angle steps spiraling outward from you, filling the field like a sunflower head with lingering hits |
| **2** (Binary) | You **split into two smaller copies** orbiting each other, like a binary star. Two attack sources, each with half the stats. |
| **ℵ₀** (Countable infinity) | Every **kill re-fires your attack from the corpse**, so chain reactions run through dense waves |
| **ε** (Infinitesimal) | You shrink to almost nothing and become hard to hit. Your attack breaks into a **dust of countless micro-hits**. |

---

## 7. Pulls: Rifts

- **Prisms** come only from playing: Thresholds, milestones, Codex completions, daily local-clock bonuses. Generous.
- **What you pull:** gear, Forms.
- **Pity** is shown on screen and carries across banners: Imaginary+ guaranteed by 30 pulls, Complex by 90.
- **Banners** rotate weekly on the local clock.
- **The reveal:** a singularity collapses and then unfolds *into as many dimensions as the rarity*: point, line, plane, solid. Complex shatters the glass UI around it.
- There's x1, x10, and a skip-to-results grid.

---

## 8. Shallow completable systems

Every completion gives a **small permanent bonus**.

| System | What you complete | Reward |
|---|---|---|
| **Archive** | Enshrine gear you've outleveled. It floats in glass cases in a 3D gallery. | +tiny global stat per item (perfect ×3). Full sets unlock a pedestal plus a bigger bonus. |
| **Set Codex** | Find every piece of every set | Set-themed cosmetic |
| **Perfection Codex** | Get a perfect copy of every piece | Gold Archive pedestals |
| **Forms Codex** | Every Form per dimension | +% to that dimension's attack |
| **Bestiary** | Kill milestones per enemy shape × color (10 / 100 / 1k / 10k / 100k) | +damage vs that type |
| **Fractal Codex** | Every Cell fractal at max recursion | Global bonus |
| **Constants** | Own every Constant; reveal every digit | Euler's Identity (§6.3), plus a permanent bonus per completed Constant |
| **Theorems** | Achievements as "proofs" | Prisms, titles |
| **Lattice** | Permanent upgrade graph (§10) | Region bonuses |

### Red dot rules
- A red dot only means there's something to do right now.
- Dots roll up the tree (tab → panel → card). Every one clears in 2 taps or fewer.
- Clearing one is physical: a glass droplet pops with a tone and a haptic tick, and the pitch goes up as you chain clears.
- **Long-press a tab** to cascade-clear its whole subtree.

---

## 9. How the player is drawn

### 9.1 Everything on the player
- **The Form**, tinted by your color mix
- **Vertex** traits on the corners (up to 3 with Harmonics: glint + trail + travelling light)
- **Weave** traits on the edges (up to 3 with Harmonics: pattern + count + shape)
- **Shell** effect on the faces
- **Cell** fractal inside, seen through the faces

That's everything on the body. Each slot only touches its own part of the shape, so nothing competes for the same pixels. **Constants change the attack, not the body.** Equip π and you can see the attack orbiting you.

### 9.2 Inspect view
The **Form screen** shows the player large, and you can pinch-zoom and rotate it.

---

## 10. Permanent upgrades: the Lattice

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

## 11. UI / UX

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

## 12. Enemies

Every enemy is a **shape × color** combination. The shape decides how it behaves, and the color decides what it resists.
- **Swarm points** (fast, many). Best answer: Pulse.
- **Sweepers**: rotating lines. Best answer: Laser.
- **Splitting polygons** (an n-gon breaks into (n−1)-gons when killed). Best answer: Pulse or Clone.
- **Shells**: polyhedra with faces you break one at a time. Best answer: Clone (multi-hit).
- **Anomaly bosses**: Möbius strip, Klein bottle, torus knot, Lorenz attractor. Best answer: Dot or Clone.
- **Elites** roll random modifiers (shielded, splitting, hasted) and drop extra loot. White elites resist every color.

---

## 13. Tech plan

**TypeScript + WebGL2, packaged as an Android app with Capacitor.**

- **Vite + TypeScript**
- **three.js** for the scene + **custom GLSL** for glass, fields, and bloom
- **SolidJS** for UI
- **Glass layer:** DOM for layout and crisp text; a WebGL pass underneath draws all glass shapes and refracts the game through them
- **Simulation:** fixed timestep, deterministic, seeded RNG, separate from rendering. The same sim runs headless for balance scripts and offline progress.
- **Content:** items, affixes, sets, Forms, fractals, and Constants live in typed data tables
- **Feature modules** (§16.3): each feature is a self-contained module that registers with the core. The core never imports features. That's what makes a forever game maintainable.
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

## 14. Roadmap

| Milestone | Goal | Done when |
|---|---|---|
| **M0: Glass spike** | Prove the UI on the real device | Liquid-glass dock + sheet refracting an animated geometry field at 120 fps on the S25 Ultra |
| **M1: Core loop** | Point + Dot attack, enemies, Depth, Flux, save/load | Can idle-farm with auto-Depth |
| **M2: Gear** | Vertex + Weave slots, drops, affixes, reforge, auto-salvage | Items show on the body and change the attack |
| **M3: Collections** | Red-dot system, Bestiary, Archive, Codex | Clearing dots feels great |
| **M4: Dimensions 1–3** | Laser, Pulse, Clone, Shell + Cell, RGB, Rifts, Lattice | Can ascend to 3D with all four attacks |
| **M5: Depth content** | Sets, color-themed Layers, bosses | Systems complete. **Decide on 4D here.** |
| **M5.5: Relics** | Euler's five Constants, Threshold boss drops, digit leveling, Euler's Identity | All five playable, second slot unlockable |
| **M6: Ship to phone** | Offline progress, Capacitor APK via CI, haptics, audio, balance pass | Installed APK on the S25 Ultra |
| **M7+: Forever** | Pull from the backlog (§16.4), alternating modular and integrated | Never "done" |

---

## 15. Open questions / agenda
1. **Shell:** Exploded and Stained confirmed. Third trait: Absorb proposed (§4.2).
2. **Collections:** the Synergy Codex is gone, but you want a collection system for *something*. What should be collected? Still open.
3. **Cell fractals:** the list, and what each one does. Next after Shell.
4. **Sets:** 2- and 4-piece bonuses that change how something works, not +X%.
5. **Enemies + Layers:** to discuss later. Threshold bosses every 100 Depth guarding Constants is confirmed.
6. **Lattice:** liked; details later.
7. **4D:** parked until M5.

---

## 16. Feature structure: modular vs integrated

### 16.1 Definitions
| Type | Meaning | Rules |
|---|---|---|
| **Core** | The backbone. Can't be turned off. | Depth farm, Forms + attacks, 4 gear slots + affixes, currencies, red dots, glass UI, save |
| **Modular** | Fully independent. Can be **switched off in Settings → Features** without breaking anything. | Depends only on core. **Nothing else depends on it.** Pays out through the generic reward system (currency, cosmetics, permanent stats). Has its own save section, tab or card, and red-dot source. |
| **Integrated** | Changes or extends other systems on purpose. | Declares its dependencies. Can't be turned off. May depend on core or on other integrated features, **never on a modular one.** |

Keeping that last rule strict means a modular feature can always be removed safely.

### 16.2 Current ledger
| Feature | Type | Depends on |
|---|---|---|
| Dimensional Ascension | Integrated | Forms, Thresholds |
| RGB damage types | Integrated | Gear affixes, enemies |
| Rarity + rerolling | Integrated | Gear |
| Sets | Integrated | Gear |
| Harmonics | Integrated | Vertex + Weave items, Lattice |
| Constants | Integrated | Thresholds, attacks |
| Euler's Identity | Integrated | Constants |
| Archive + Perfection Codex | Integrated | Gear |
| Lattice | Integrated | Currencies |
| Rifts | Integrated | Gear, Forms |
| Fractal Cell + Codex | Integrated | Cell slot |
| **Bestiary** | **Modular** | — |
| **Theorems** | **Modular** | — |

Right now it leans heavily integrated, which is normal: the foundation has to be built first. **The backlog leans modular to even things out.**

### 16.3 How modules plug in
Every feature, of either type, uses the same contract:
- **Stat contributions:** "+X% damage", new multiplier types
- **Event hooks:** on kill, on hit, on wave, on Depth change, on Threshold clear, on return from offline
- **Red-dot provider:** "what's actionable in this feature right now"
- **UI entry:** a tab, a card in a hub screen, or a section in an existing screen
- **Save section:** its own versioned namespace, so adding or removing a feature never breaks the save
- **Data tables:** its content

A **Features** screen in Settings lists every modular feature with an on/off switch. Turning one off pauses its bonuses and hides its UI. Turning it back on resumes it exactly where it was.

### 16.4 Backlog

**Modular**
| Idea | What it is |
|---|---|
| **Tessellation** | A Penrose tile board. Tiles drop from kills, and completed patterns give permanent bonuses. |
| **Observatory** | Stars appear in the void's background as you kill. Connect them into constellations to fill a star chart. |
| **Fractal Garden** | Grow L-system plants (ferns, trees, dragon curves) in real time and harvest them for Shards. Species codex. |
| **Daily Proof** | A short daily geometry puzzle (tangram, slide, dissection) for Prisms |
| **Resonance** | Unlock scales and modes for the procedural soundtrack. A music collection. |
| **Spirograph Studio** | Compose your Comet trails into still images. Cosmetic gallery. |
| **Void Weather** | Random timed events: *Eclipse* (every enemy turns blue for 10 min), *Meteor shower* (loot rain), *Aurora* (double Prisms) |
| **Knots** | An untangle puzzle that uses real knot diagrams, with a knot codex |

**Integrated**
| Idea | Depends on | What it is |
|---|---|---|
| **Form Mastery** | Forms | Each Form levels with use and unlocks a perk unique to that Form |
| **Conjectures** | Forms, RGB, gear | Permanent side Depths with constraints (1D only, single color, no Shell). No resets, and the rewards are permanent. |
| **Imprinting** | Archive, gear | Copy a trait from an enshrined item onto a new one |
| **Constant Proofs** | Constants | A small tuning tree per Constant |
| **Expeditions** | Forms | Send Forms you aren't using on timed trips into old Layers for loot |
| **4D** | Ascension, Forms | The capstone dimension, if kept |
