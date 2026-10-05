# Ventris — Design Plan (draft 1)

> Working title. Idle tower defense where **you are the tower**, an abstract shape in a pitch-black void.
> It levels up for good: no prestige, no resets, no upkeep. Every piece of gear you equip shows up on the shape.

---

## 1. Pillars

These are the rules every feature has to pass.

1. **Permanent.** Nothing ever resets. Each upgrade, unlock, and collection entry stays forever.
2. **Zero upkeep.** No durability, stamina, energy, or repair costs. Any chore gets automated or cut.
3. **You see what you wear.** Every equipped item draws something on the player, and item visuals combine in layers (like Binding of Isaac).
4. **Lots of RNG, all of it fun.** Drops, affix rolls, rerolls, and pulls. Bad luck is softened by pity counters and the Archive (§7). It's never punished.
5. **Small things to finish.** Many shallow systems you can 100%, each with its own red dots and a completion moment.
6. **UI that makes people stop and look.** The interface is liquid glass that bends the live game behind it. More on this in §10.
7. **Pure math visuals.** Everything is generated from geometry: polygons, polytopes, fractals, curves, SDFs. There are no hand-made art assets.

**Closest reference:** *The Tower* (Tech Tree Games) is also a "you are the tower" idle TD, but it's built around runs that reset. Ventris drops runs completely: one continuous farm where you choose how deep to push.

---

## 2. Core loop

```
 ┌─────────────── seconds ───────────────┐
 │ Shapes stream in from the void → you  │
 │ shoot them → Flux + loot pop out       │
 └───────────────────┬───────────────────┘
                     ▼
 ┌─────────────── minutes ───────────────┐
 │ Equip / roll / reforge gear, pull     │
 │ Rifts, buy Lattice nodes, clear dots  │
 └───────────────────┬───────────────────┘
                     ▼
 ┌──────────────── hours ────────────────┐
 │ Push Depth, finish sets, unlock Forms,│
 │ fill Codex pages                      │
 └───────────────────┬───────────────────┘
                     ▼
 ┌──────────────── days+ ────────────────┐
 │ Dimensional Ascension (0D→1D→…→nD),   │
 │ perfect sets, enshrine in the Archive │
 └───────────────────────────────────────┘
```

### Depth (the farm)
- There are no levels. Depth is one number that goes from 1 to ∞, and enemy HP/damage/count grow exponentially with it.
- **Auto-Depth (on by default):** if you clear a wave fast enough you go down one Depth. If the void breaches your Integrity, you get pushed back up a few Depths. You never lose anything, and there's no fail screen.
- You can lock Depth to farm one spot, e.g. a Layer that drops a certain set.
- Every **10 Depth** is a new *Layer* with a new enemy palette and loot table. Every **100** is a *Threshold* with a boss Anomaly.
- **Offline progress** pays your measured clear rate at your locked or auto Depth, up to a cap. When you come back you get a "while you were gone" glass card that you swipe to collect, with loot raining out of it.

### Optional active layer
The game is idle, but give the player something to do with their thumbs:
- **Collapse**: tap the field to drop a singularity that pulls enemies in. Has a cooldown and an auto toggle.
- **Drag to tilt**: rotates the Form so a vertex-heavy side faces a dense wave. Has auto-aim.
- Everything active can be automated. Active play is a bit better than idle, not required.

---

## 3. The player: Dimensions × Forms

Your two "what is the player?" ideas fit together: **you are the shape, and each new dimension is a major feature unlock.**

### 3.1 Dimensional Ascension (macro progression, never resets)

| Dim | You are | Combat change | Unlocks |
|---|---|---|---|
| **0D** | A point | Fires single pulses | Emitter slot, Flux, Bestiary. About 10 min of tutorial. |
| **1D** | A line segment (spins) | Fires from both ends, beam attacks | Lens + Trace slots, gear drops & affix rolling |
| **2D** | A polygon | Each vertex is a mount | Orbit + Field slots, **Forms (polygons)**, RGB color system, **Rifts** (pulls) |
| **3D** | A polyhedron | Vertices, edges, and faces all matter (§3.3) | Shell + Resonator slots, **Platonic/Archimedean Forms**, Fractal Echoes, **Archive** |
| **4D** | A 4-polytope, shown rotating through W | Phase mechanics: shots/enemies slide in and out of 3-space | Glyph slot, 4-polytope Forms |
| **5D+** | n-cube / n-simplex / n-orthoplex projections | Each dimension adds one stat axis and one passive | Never ends. It's the infinite progression axis that replaces prestige. |

Ascending takes a Threshold boss kill plus a small collection requirement, like "own 3 Forms of the current dimension". It's a big ceremony: the camera pulls back while your shape extrudes into the next dimension.

Higher-dimensional shapes are all generated from math. n-cube vertices are just {±1}ⁿ, projected along a Petrie polygon, so we never run out of content.

### 3.2 Forms (collectible bodies)
- **2D:** triangle → square → … → dodecagon, then the circle as the limit (the "∞-gon" is a rare unlock).
- **3D:** the 5 Platonic solids first, then the 13 Archimedean solids, then the Catalan duals.
- **4D:** the 6 regular convex 4-polytopes (5-cell, tesseract, 16-cell, 24-cell, 120-cell, 600-cell).
- You unlock each Form once and can swap between them freely. No reset and no swap cost.

### 3.3 Geometry is the stat system
Each Form's V/E/F counts feed straight into combat:
- **Vertices** are fire points, so more vertices means more projectiles per volley.
- **Edges** are links. Chain, beam, and synergy effects travel along them.
- **Faces** are shield panels. Each face is a separate damage-absorbing plate.

That makes **duals a real build choice:** cube (8V / 12E / 6F) is offense, octahedron (6V / 12E / 8F) is defense. Same for dodecahedron vs icosahedron. Tetrahedron is its own dual and acts as the balanced pick. Euler's V − E + F = 2 keeps it self-balancing for free.

---

## 4. Gear

### 4.1 Slots (each is its own visual layer, see §8)

| Slot | Unlocks at | Does | Draws as |
|---|---|---|---|
| Emitter | 0D | Base attack type (pulse, beam, shard, wave) | Glyphs mounted on every vertex |
| Lens | 1D | Projectile modifiers: split, pierce, homing, ricochet | Changes projectile shape and trail |
| Trace | 1D | What's left behind: trails, mines, afterimages | Ribbons / dotted paths |
| Orbit | 2D | Satellites, rings | Concentric rings and orbiting bodies |
| Field | 2D | Aura: slow, burn, pull | Shader field around you (ripples, voronoi, moiré) |
| Shell | 3D | Defense, Integrity, thorns | Glass panels over faces |
| Resonator | 3D | Color affinity (RGB, §5) | Tints and emissive veins |
| Glyph | 4D | Economy: loot, Flux, rarity find | Sigil floating above the Form |

### 4.2 Rarity (themed on number sets)
**Integer → Rational → Irrational → Transcendental → Imaginary → Complex**

Higher rarity gives more affix lines, higher roll ceilings, and better-looking glass (more refraction, caustics, and prismatic dispersion).

### 4.3 Affixes and rolling
- Each item gets 1–6 affix lines rolled from its slot's pool. Each line has a **tier (T1–T10)** and a **roll within that tier's range**.
- **Perfect line** = top tier and max roll. **Perfect item** = every line perfect. Perfect items get a permanent visual shimmer.
- Sample affixes: damage %, fire rate, range, crit chance/dmg, projectile count, pierce, chain, split, homing strength, area, Integrity, regen, shield per face, R/G/B affinity, Flux gain, loot luck, rarity find.

### 4.4 Rerolling (the RNG sink)
| Action | Cost | Effect |
|---|---|---|
| **Reforge** | Shards | Reroll the value of one line inside its tier |
| **Retier** | Shards + Flux | Reroll one line's tier |
| **Transmute** | Prisms | Swap one line's type for a random one |
| **Lock** | Extra cost per locked line | Protect lines during a full reroll |
| **Full reroll** | Shards | Reroll every unlocked line |

Every roll animation is fast, skippable, and readable: numbers spin like a slot machine, then snap into place with a haptic tick. Perfect rolls get their own sound and flash.

### 4.5 Sets (using real math sets)
Each Layer band has its own set: **Cantor Set, Julia Set, Mandelbrot Set, Borel Set, Power Set, Vitali Set**, and as an endgame joke, the **Empty Set** (its bonus scales with how *few* slots you fill).

- Each set has 8 pieces (one per slot) with bonuses at 2, 4, and 8 pieces.
- Each piece has a fixed visual motif. A full set turns your silhouette into something new, e.g. the full Cantor Set makes the Form shatter into a self-similar dust cloud.

### 4.6 Duplicates
Duplicates are never dead loot. A duplicate set piece **Echoes** into the one you own, adding +1 star (★1–★5). Each star raises roll ceilings and adds a visual flourish.

---

## 5. Color: RGB additive damage

The background is pure black and projectiles use additive blending, so **colors mix for real on screen.** We use that as a mechanic:

- There are three primary damage frequencies: **Red** (burn/DoT), **Green** (chain/spread), **Blue** (slow/shatter).
- When two colors overlap on the same enemy, they make a secondary color with its own effect:
  - **Yellow** (R+G): spreading burn
  - **Cyan** (G+B): frozen chain
  - **Magenta** (R+B): shatter detonates burn
- **White** (R+G+B) triggers *Annihilation*, a big proc.
- Resonator gear and affinity affixes set your color mix. The visuals are the game state: if you see magenta flashes, the magenta combo is firing.

---

## 6. Pulls: Rifts

- **Currency:** Prisms, earned only by playing. They drop from Thresholds, milestones, Codex completions, and daily local-clock bonuses. There's no store and no IAP for now.
- **What you pull:** gear, Forms, Fractal Echoes, Constants (§7).
- **Pity:** shown on screen. Guaranteed Imaginary+ at 50 pulls, Complex at 150. The counter carries over between banners.
- **Banners** rotate on the local clock (weekly) and feature one set or one Constant.
- **The reveal is the reward.** A singularity collapses, then unfolds *into as many dimensions as the rarity*: Integer stops at a point, Rational stretches into a line, and so on up to Complex, which unfolds into a spinning tesseract and shatters the glass UI around it. Rarity shows up a beat before the item does, the way gacha games build tension.
- There's x1, x10, and a "skip to results" grid for big pulls.

---

## 7. Shallow completable systems

Each one is a small checklist with red dots, a completion %, and a reward when finished. **Every completion gives a small permanent bonus**, so collecting always adds power, which matters in a game with no prestige.

| System | What you complete | Completion reward |
|---|---|---|
| **Archive** | Enshrine gear you've outleveled. Rotating glass display cases float in a 3D gallery. | Each enshrined item: +tiny global stat. Perfect items count ×3. Full sets unlock a pedestal plus a bigger bonus. |
| **Set Codex** | Find every piece of every set | Set-themed cosmetic trail |
| **Perfection Codex** | Roll a perfect copy of every piece | Gold-tier Archive pedestal |
| **Forms Codex** | Unlock every Form per dimension | +% to that dimension's V/E/F effects |
| **Bestiary** | Kill milestones per enemy type (10 / 100 / 1k / 10k / 100k) | +damage vs that type, plus lore in math-flavored nonsense |
| **Constants** (relics) | Collect π, e, φ, √2, i, γ, Feigenbaum δ, … | Each is a passive that **changes visuals too**. φ curves projectiles into golden spirals. π makes orbits perfectly circular and boosts Orbit damage. *i* rotates shots 90° partway through flight. |
| **Fractal Echoes** (companions) | Sierpiński, Koch snowflake, Menger sponge, Dragon curve, Barnsley fern, … | **Leveling up adds a recursion depth**, so the companion gets visibly more detailed |
| **Theorems** (achievements) | "Proofs" of feats, e.g. *Pigeonhole: kill 10 enemies with 9 projectiles* | Prisms and titles |
| **Synergy Codex** | Find named item combos, like Isaac's transformations (e.g. Lens:Split + Orbit:Ring = **Rosette**) | Each discovery is permanent, so later combos auto-highlight |
| **Lattice** | Permanent upgrade graph (§9) | Fill a whole region of the tessellation to get its region bonus |

### Red dot rules
- A red dot only shows up when there's **something to do right now.** No informational dots, because those wear people out fast.
- Dots roll up the tree (tab → panel → card) and **every dot clears in 2 taps or fewer.**
- Clearing one feels physical: a glass droplet pops, makes a short pitched tone, and plays a haptic tick. Pitch goes up the more you clear in a row (a combo).
- A **"Collect all"** gesture (long-press a tab) clears a whole subtree in one cascading chain, which feels really good.

---

## 8. Visual composition (the Isaac part)

The player is drawn as stacked procedural layers, and **each equipped item adds to one or more of them**:

```
 L7  Glyph sigil            (above)
 L6  Field shader           (aura, screen-space)
 L5  Orbit rings/bodies
 L4  Shell panels on faces
 L3  Emitters on vertices
 L2  Core Form              (wireframe + glass faces)
 L1  Resonator veins/tint
 L0  Trace / trail          (world-space, behind)
 ── projectiles get Emitter base × Lens modifiers × Constant transforms × color
```

**How combos stay readable:**
- Each item adds **parameters** instead of sprites. That means things like ring radius, ring count, glyph shape id, rotation speed, color weight, and noise frequency.
- Items in the same layer **stack by rules.** Two Orbit items make two rings at different radii spinning in opposite directions. Two Field items show a **moiré interference pattern** where they overlap, which happens naturally when you overlay two periodic fields.
- **Tag rules** handle the Isaac-style transformations. If an equipped set of tags matches a rule (e.g. `{split, ring}` → Rosette), an override visual and bonus kicks in, and its Synergy Codex entry gets unlocked.
- **Visual budget:** the in-combat Form is small on a phone, so layers get LOD. Full detail is shown on the **Form screen**, where you can pinch-zoom and rotate the player like a museum piece.

Projectiles work the same way. Homing gives a curved trail, split leaves fractal children, chain draws lightning along edges, and φ bends everything into golden spirals. Combine all four and you get something nobody designed by hand.

---

## 9. Permanent upgrades: the Lattice

- A big node graph laid out as a **Penrose / hex tessellation** that keeps expanding outward. It's bought with **Axioms**, a rare currency from Thresholds and milestones.
- Nodes are permanent and never refunded or reset. Better nodes are farther out, and more of the graph shows up with each Dimension.
- Finishing a region (a closed tile shape) grants a region bonus, which makes it another small thing to complete.

### Currencies (keep this short)
| Currency | Source | Spent on |
|---|---|---|
| **Flux** | Every kill | Base stat upgrades, item leveling |
| **Shards** | Salvaging gear | Reforge / reroll |
| **Prisms** | Milestones, Thresholds, Codex | Rifts, Transmute |
| **Axioms** | Thresholds, rare drops | Lattice |

Four currencies, and each has exactly one job.

### Automation (so there's no upkeep)
- Auto-collect drops, auto-equip upgrades (with a "never replace locked" toggle), and auto-salvage by rarity/affix filters.
- Auto-Depth, auto-Collapse, and auto-claim for offline progress.
- There's nothing to repair, refuel, or maintain.

---

## 10. UI / UX: "never seen UI like this"

### Look
- A **true #000 background** (looks great on OLED). The only light comes from the game itself.
- **Liquid glass panels with real refraction.** Panels sample the live game framebuffer behind them and displace it based on the SDF edge gradient. The middle stays mostly clear, while the edges bend the scene like a thick lens. They also get:
  - **chromatic dispersion** at the rims, splitting RGB slightly
  - **frosted blur** that varies by panel "thickness"
  - a **specular highlight that follows the device gyroscope**, so tilting the phone moves light across all the glass
  - **liquid merging:** panels blend into each other with smooth-min SDFs. A button splitting off a dock stretches and pinches off like a droplet instead of just appearing.
- When menus cover the game, a faint drifting field of geometry stays behind the glass so it always has something to bend.

### Feel
- Everything animates with **spring physics** and nothing uses linear easing. Every gesture can be interrupted midway (grab a sheet while it's opening and it follows your finger).
- **Haptics on every meaningful tap**, with different patterns for rarity, perfect rolls, and red-dot clears.
- **Procedural audio:** WebAudio synthesis with every sound tuned to one musical key. Kills play pentatonic notes, so heavy combat sounds like an arpeggio.
- Bottom-sheet navigation over the **live, still-running battle**. You never leave the game; panels just pour over it.
- Damage numbers, loot beams colored by rarity, and roll results are made to be legible at a glance first and flashy second.

### Main screens
| Tab | Contents |
|---|---|
| **Void** (home) | Battle, Depth indicator, Collapse button, mini red-dot dock |
| **Form** | 3D inspectable player, slots, Form/Dimension swap |
| **Arsenal** | Inventory, reforge bench, filters, auto-salvage rules |
| **Rift** | Banners, pulls, pity |
| **Lattice** | Permanent upgrade graph |
| **Archive** | Gallery, Codex, Bestiary, Constants, Theorems |

---

## 11. Enemies

All of them are abstract and generated:
- **Swarm points** (0D) that come in fast and in large numbers
- **Sweepers** (1D): lines that rotate across the field
- **Polygons** that **split into smaller polygons** when killed (n-gon → n−1-gons)
- **Shells**: polyhedra with armored faces you have to break one at a time
- **Phasers** (4D+): only take damage while they're crossing your 3-slice
- **Anomaly bosses** at Thresholds: Möbius strip, Klein bottle, torus knot, Hopf fibration, Lorenz attractor
- **Elites** roll random modifiers too (shielded, splitting, hasted), and they drop more loot. Yes, the enemies get RNG as well.

---

## 12. Tech plan (recommendation)

**TypeScript + WebGL2, packaged with Capacitor for iOS/Android.**

Why this over Unity/Godot:
- The UI is the selling point, and **DOM/CSS for layout and text + a WebGL glass layer underneath** is the quickest path to crisp text and shader-driven glass.
- Everything is procedural, so there are no art pipelines to build. It's all code.
- It's fast to iterate on: hot reload, test on a phone through a browser right away, and screenshot tests in headless Chromium.
- Capacitor gives native haptics, gyroscope, and app store packaging.

Stack:
- **Vite + TypeScript**
- **three.js** for the scene (polyhedra, instancing for thousands of projectiles) plus **custom GLSL** for glass, fields, and post-processing (bloom on black)
- **SolidJS** for UI (fine-grained reactivity handles hundreds of live-updating numbers without re-render cost)
- **Glass layer:** a full-screen canvas pass. UI components register their rects and corner radii, the shader renders the SDF union of all glass shapes refracting the game buffer, and the DOM text sits on top.
- **Simulation:** fixed-timestep, deterministic, seeded RNG, separate from rendering. The same sim runs headless for **balance scripts** (time-to-Depth curves, drop-rate checks) and offline progress.
- **Data-driven content:** items, affixes, sets, Forms, and Constants live in typed tables.
- **Save:** IndexedDB with a versioned schema and migrations, plus export/import of a save string.

Risks:
- **Glass refraction cost on low-end Android:** sample the scene at half resolution and fall back to blur-only.
- **Visual noise with many items:** layer LOD and the visual budget from §8.
- **Endless power growth with no prestige:** balance in log space. Each Dimension and Layer adds new multiplier *axes* instead of bigger numbers on old ones, and the headless sim catches bad curves early.

---

## 13. Roadmap

| Milestone | Goal | Done when |
|---|---|---|
| **M0: Glass spike** | Prove the wow factor and performance | A liquid-glass dock + sheet refracting an animated geometry field at 60 fps on a real phone |
| **M1: Core loop** | Tower, enemies, projectiles, Depth, Flux, save/load | Can idle-farm and auto-Depth |
| **M2: Gear** | Slots, drops, affixes, reforge, auto-salvage, layered visuals v1 | Gear changes how you look and how you play |
| **M3: Collections** | Red-dot system, Bestiary, Archive, Codex | Clearing dots feels great |
| **M4: Dimensions 0–3** | Forms, V/E/F stats, RGB colors, Rifts | Can ascend to 3D |
| **M5: Depth content** | Fractal Echoes, Constants, Lattice, Synergies, 4D | Systems are complete |
| **M6: Ship prep** | Offline progress, Capacitor builds, haptics, audio, balance pass | Runs on iOS + Android |

---

## 14. Open questions
1. iOS, Android, or both? (Affects how much the gyroscope/haptic polish matters, plus test devices.)
2. Portrait-only? (I'm assuming yes for one-handed idle play.)
3. Monetization later, or never? Pity and pull rates should be designed honestly either way. If IAP might come later, the economy should be built to allow it without a rework.
4. Is the RGB color system too much on top of everything else, or is it the main hook?
5. Should active play (Collapse, tilt) stay optional, or matter more?
