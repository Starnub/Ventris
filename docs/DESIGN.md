# Ventris — Design Plan (draft 2)

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
| Gear visuals | Every item has **one clear, distinct signature effect**, and each slot gets its own visual channel so effects never pile up (§8). |
| Dimensions | **Finite.** 0D → 1D → 2D → 3D, with 4D possibly as a final capstone (§3.2). No infinite n-D. |

---

## 1. Pillars

1. **Permanent.** Nothing ever resets.
2. **Zero upkeep.** No durability, stamina, energy, or repairs. Chores get automated or cut.
3. **You see what you wear.** Each item puts one readable effect on the player, and effects combine without turning into noise.
4. **Lots of RNG, all of it fun.** Drops, affix rolls, rerolls, pulls. Bad luck is softened by generous pity and the Archive, never punished.
5. **Small things to finish.** Many shallow systems you can 100%, each with its own red dots and a completion moment.
6. **The menus are the game.** The game is played in menus, so they need to feel better than any menu you've used.
7. **Pure math visuals.** Everything is generated geometry. No art assets.

**Closest reference:** *The Tower* (Tech Tree Games), but with no runs. It's one continuous farm.

---

## 2. Core loop

```
 seconds  │ Shapes stream in → the tower auto-fires → Flux + loot pop out
 minutes  │ Equip / roll / reforge, pull Rifts, buy Lattice nodes, clear dots
 hours    │ Push Depth, finish sets, unlock Forms, fill Codex pages
 days+    │ Ascend a dimension, perfect sets, enshrine in the Archive
```

### Depth (the farm)
- Depth is one number from 1 to ∞. Enemy HP, damage, and count grow exponentially with it.
- **Auto-Depth (default):** clear waves fast enough and you go one Depth deeper. If the void breaches your Integrity, you get pushed back up a few Depths. Nothing is lost and there's no fail screen.
- **Depth lock** lets you farm a specific Layer, e.g. the one that drops the set you're chasing.
- Every **10 Depth** is a new *Layer* with new enemies, a new loot table, and eventually **a new multiplier type**. Every **100** is a *Threshold* with a boss Anomaly.
- **Offline progress** pays your measured clear rate, with a generous cap since this is just for you. On return you get a glass "while you were gone" card that you swipe to collect.

### Where the decisions happen
Combat runs itself, so all player choice lives in menus:
- **Loadout presets** (e.g. "Push" vs "Farm loot"), swapped in one tap. Auto-Depth can switch between them on its own if you set a rule.
- Choosing a Form (the V/E/F tradeoff in §3.3).
- Gear choices, roll chasing, and set building.
- Lattice routing.
- Depth lock targets for farming.

---

## 3. The player: Dimensions × Forms

You are the shape. Each new dimension is a major permanent unlock that gives new slots, new mechanics, a new silhouette, and new multiplier types.

### 3.1 Dimensional Ascension

| Dim | You are | Combat change | Unlocks |
|---|---|---|---|
| **0D** | A point | Single pulses | Emitter slot, Flux, Bestiary. About 10 min of tutorial. |
| **1D** | A spinning line segment | Fires from both ends, beams | Weave + Lens slots, gear drops and affix rolling |
| **2D** | A polygon | Each vertex is a mount | Orbit + Field slots, **Forms (polygons)**, **Rifts** |
| **3D** | A polyhedron | Vertices, edges, and faces all count (§3.3) | Shell slot, **Platonic → Archimedean Forms**, Fractal Echoes, **Archive** |
| **4D?** | A 4-polytope rotating through W | *Phase*: projectiles pass in and out of 3-space, ignoring armor | No new slot. Just the capstone Forms and the phase mechanic. |

Ascending takes a Threshold boss kill plus a small collection requirement (e.g. own 3 Forms of the current dimension). It's a big ceremony: the camera pulls back while your shape extrudes into the next dimension.

### 3.2 Should 4D stay?
**My take: keep it as a capstone, but only with the clean polytopes.**

- **For:** a tesseract rotating through itself is *the* image of "dimensions." Without it, the theme ends on a cube, which is a bit of a letdown after three ascensions.
- **Against:** 4D gets noisy fast. The 120-cell has 600 vertices and 1200 edges, and the 600-cell has 720 edges. Those turn into a hairball on a phone screen.
- **Compromise:** 4D gets only the **5-cell, tesseract, and 16-cell** (maybe the 24-cell). The two huge ones are cut. That's 3–4 Forms, all of which read clearly.
- **No rush to decide.** 4D is the last thing on the roadmap and nothing before it depends on it. Build 0D–3D, look at it on the S25 Ultra, then decide. If 4D gets dropped, 3D with Archimedean/Catalan Forms becomes the endgame and nothing else changes.

### 3.3 Forms (collectible bodies)
- **2D:** triangle → … → dodecagon, then the circle as a rare limit unlock.
- **3D:** 5 Platonic solids, then 13 Archimedean, then their Catalan duals.
- **4D (if kept):** 5-cell, tesseract, 16-cell (24-cell maybe).
- You unlock each Form once and swap freely, with no cost.

### 3.4 Geometry is the stat system
- **Vertices** are fire points, so more vertices means more projectiles per volley.
- **Edges** are links. Chain and beam effects travel along them.
- **Faces** are shield plates. Each one absorbs damage separately.

**Duals are a build choice:** cube (8V / 6F) is offense, octahedron (6V / 8F) is defense. Dodecahedron vs icosahedron works the same way, and the tetrahedron is its own dual, so it's the balanced pick.

---

## 4. Gear

### 4.1 Six slots, six visual channels
Each slot **owns one visual channel**, so two items can never fight over the same part of the player.

| Slot | Unlocks | Gameplay role | Visual channel | Example signature effects |
|---|---|---|---|---|
| **Emitter** | 0D | Attack type | **Vertex ornaments** | spike, ring, tiny cube, star |
| **Weave** | 1D | Firing rhythm | **Line style** (edges + trails) | solid, **dotted**, dashed, double, braided |
| **Lens** | 1D | Projectile behavior | **Projectile shape** | needle, droplet, prism, crescent |
| **Orbit** | 2D | Satellites | **Orbital bodies** | **one orbiting sphere**, twin moons, ring, shard belt |
| **Field** | 2D | Aura effect | **Space around you** | ripple rings, bent grid, halo, still void |
| **Shell** | 3D | Defense | **Face fill** | hollow, frosted glass, mirror, pulsing |

**Visuals match mechanics wherever possible**, so you can read the build by looking at it:
- **Dotted** Weave = burst fire (the gaps are the pauses). **Dashed** = piercing segments. **Double** = twin shots.
- One orbiting **sphere** = a single heavy satellite. **Shard belt** = many weak ones.
- **Mirror** Shell = reflects projectiles. **Frosted** = damage reduction.

Economy stats (Flux gain, loot luck, rarity find) are affix lines that can roll on any piece. They don't get a slot.

### 4.2 Rarity: number sets
**Integer → Rational → Irrational → Transcendental → Imaginary → Complex**

Higher rarity means more affix lines and higher roll ceilings. Visually, **rarity changes the quality of an effect, not how many effects there are.** An Integer sphere is a flat white dot. A Complex sphere is refractive glass with caustics. Still one sphere either way.

### 4.3 Affixes and rolling
- 1–6 affix lines per item, rolled from that slot's pool. Each line has a **tier (T1–T10)** and a **roll within the tier's range**.
- **Perfect line** = top tier and max roll. **Perfect item** = every line perfect, which adds a subtle permanent shimmer.
- Sample affixes: damage %, fire rate, range, crit chance/dmg, projectile count, pierce, chain, split, homing, area, Integrity, regen, shield per face, R/G/B affinity, Flux gain, loot luck, rarity find.

### 4.4 Rerolling (the RNG sink)
| Action | Cost | Effect |
|---|---|---|
| **Reforge** | Shards | Reroll one line's value within its tier |
| **Retier** | Shards + Flux | Reroll one line's tier |
| **Transmute** | Prisms | Swap one line's type |
| **Lock** | Extra cost per lock | Protect lines during a full reroll |
| **Full reroll** | Shards | Reroll every unlocked line |

Roll animations are fast and skippable: numbers spin like a slot machine, then snap into place with a haptic tick. Perfect rolls get their own sound and flash.

### 4.5 Sets (real math sets)
**Cantor Set, Julia Set, Mandelbrot Set, Borel Set, Power Set, Vitali Set**, plus the endgame **Empty Set**, whose bonus grows the fewer slots you fill. Visually it's the one build that strips the player back down to a bare shape.

- Sets have 6 pieces (one per slot), with bonuses at 2, 4, and 6.
- Each piece's signature effect follows the set's motif. Wearing the full set makes the whole silhouette read as that set (e.g. every Cantor piece uses a broken, gapped style).

### 4.6 Duplicates
A duplicate **Echoes** into the copy you own, adding a star (★1–★5). Stars raise roll ceilings and polish the effect (more glow, smoother motion). They never add new effects.

---

## 5. Color: RGB additive damage *(still open: keep it or cut it?)*

On pure black with additive blending, overlapping colors really do mix on screen:
- **Red** = burn, **Green** = chain, **Blue** = slow.
- When two colors land on the same enemy, they make a secondary color: **Yellow** (spreading burn), **Cyan** (frozen chain), **Magenta** (shatter detonates burn). All three give **White**, which triggers Annihilation.
- Color comes from R/G/B affinity affixes across all your gear. Your Form is **tinted by your mix**, so color isn't a separate visual layer.

---

## 6. Pulls: Rifts

- **Prisms** come only from playing: Thresholds, milestones, Codex completions, daily local-clock bonuses. It's generous, since there's nothing to sell.
- **What you pull:** gear, Forms, Fractal Echoes, Constants.
- **Pity** is shown on screen and carries across banners: Imaginary+ guaranteed by 30 pulls, Complex by 90.
- **Banners** rotate weekly on the local clock.
- **The reveal:** a singularity collapses and then unfolds *into as many dimensions as the rarity*: a point, then a line, a plane, a solid. Complex shatters the glass UI around it. Rarity shows a beat before the item does.
- There's x1, x10, and a skip-to-results grid.

---

## 7. Shallow completable systems

Every completion gives a **small permanent bonus**, so collecting always adds power.

| System | What you complete | Reward |
|---|---|---|
| **Archive** | Enshrine gear you've outleveled. It floats in glass cases in a 3D gallery. | +tiny global stat per item (perfect ×3). Full sets unlock a pedestal plus a bigger bonus. |
| **Set Codex** | Find every piece of every set | Set-themed trail cosmetic |
| **Perfection Codex** | Get a perfect copy of every piece | Gold Archive pedestals |
| **Forms Codex** | Every Form per dimension | +% to that dimension's V/E/F effects |
| **Bestiary** | Kill milestones per enemy (10 / 100 / 1k / 10k / 100k) | +damage vs that type |
| **Constants** | π, e, φ, √2, i, γ, δ, … | All owned Constants give passive stats. **You equip one** as your signature, and that one bends your projectiles' path (φ = golden spiral, i = 90° turn mid-flight). |
| **Fractal Echoes** | Sierpiński, Koch, Menger, Dragon curve, Barnsley fern, … | **One companion is active at a time.** Leveling it up adds a recursion depth, so it visibly gains detail. |
| **Theorems** | Achievements as "proofs" | Prisms, titles |
| **Synergy Codex** | Named channel combos (§8.3) | Discovered combos stay highlighted forever |
| **Lattice** | Permanent upgrade graph (§9) | Region bonuses |

### Red dot rules
- A red dot only means there's something to do right now. Nothing purely informational gets one.
- Dots roll up the tree (tab → panel → card). Every one clears in 2 taps or fewer.
- Clearing one is physical: a glass droplet pops with a short tone and a haptic tick, and the pitch goes up as you chain clears.
- **Long-press a tab** to cascade-clear its whole subtree.

---

## 8. How the player is drawn

### 8.1 The visual budget
The most you'll ever see on the player at once:
- the **Form** itself (tinted by your color mix)
- **6 slot effects**, one per channel
- **1 Fractal Echo** floating beside it
- **1 Constant**, which only changes projectile paths, not the body

That's the hard cap, and nothing else can be added to the player.

### 8.2 How effects combine (the Isaac part)
Channels don't stack inside the player. **Projectiles inherit channels from it:**
- Projectile **shape** comes from the Lens.
- Projectile **trail style** comes from the Weave: dotted Weave gives dotted trails.
- Projectile **fill** comes from the Shell: hollow Shell gives hollow bullets.
- Projectile **path** comes from the Constant: φ gives golden spirals.

So a hollow prism with a dotted trail curling in a golden spiral is something you put together yourself, and all four of its parts are still easy to pick out.

### 8.3 Synergies
A short hand-made list of channel pairs that make a named effect. Each one gets a Synergy Codex entry and a bonus. Examples:
- **Ellipsis** (dotted Weave + sphere Orbit): the sphere leaves a dotted orbit path that damages what it touches.
- **Halo Lens** (halo Field + prism Lens): projectiles refract through the halo and split.
- **Mirror Hall** (mirror Shell + ripple Field): reflected projectiles pick up the ripple's knockback.

About 20–30 synergies in total, so each one feels like a discovery rather than one entry in a combinatorial spreadsheet.

### 8.4 Inspect view
The **Form screen** shows the player large, and you can pinch-zoom and rotate it like a museum piece. That's where the detail of each effect gets to show off.

---

## 9. Permanent upgrades: the Lattice

- An expanding **Penrose / hex tessellation** node graph, bought with **Axioms**.
- Nodes are permanent. More of the graph opens with each dimension and Layer.
- **New multiplier types live here.** Each region introduces a new multiplier (e.g. "×damage per Archive item", "×crit per face") rather than another +% on an existing stat.
- Finishing a region (a closed tile shape) gives its region bonus.

### Currencies
| Currency | Source | Spent on |
|---|---|---|
| **Flux** | Every kill | Base stats, item leveling |
| **Shards** | Salvage | Reforge / reroll |
| **Prisms** | Milestones, Thresholds, Codex | Rifts, Transmute |
| **Axioms** | Thresholds, rare drops | Lattice |

### Automation (so there's no upkeep)
- Auto-collect drops, auto-salvage by rarity/affix filters, auto-Depth, auto-claim offline progress.
- **Auto-equip is off by default.** Equipping is part of the menu gameplay. It's there if you want it.

---

## 10. UI / UX

### Look
- **True #000** (the S25 Ultra's OLED shuts those pixels off, so black is really black). The only light comes from the game.
- **Liquid glass panels with real refraction.** Panels bend the live game behind them at the edges. They also get:
  - **chromatic dispersion** at the rims
  - **frosted blur** that varies with panel thickness
  - a **specular highlight that follows the gyroscope**
  - **liquid merging:** panels blend together with smooth-min SDFs, so a button splitting off a dock stretches and pinches off like a droplet
- When menus cover the game, a faint drifting field of geometry stays behind the glass so it always has something to bend.

### Feel
- **Spring physics** on everything. Every gesture can be interrupted midway.
- **Native haptics** with distinct patterns for taps, rarity reveals, perfect rolls, and red-dot clears.
- **Procedural audio** in one musical key. Kills play pentatonic notes, so combat sounds like a soft arpeggio while you're in menus.
- **Bottom sheets over the live battle.** You never leave the game.
- **Built for the S25 Ultra screen:** 1440×3120, ~412×891 CSS px at 3.5× DPR, 120 Hz. Edge-to-edge, with safe areas for the punch-hole camera and rounded corners. Main controls sit in the bottom third for thumbs.

### Main screens
| Tab | Contents |
|---|---|
| **Void** (home) | Battle, Depth, loadout switch, red-dot dock |
| **Form** | Inspectable player, slots, Form/Dimension swap |
| **Arsenal** | Inventory, reforge bench, filters, auto-salvage rules |
| **Rift** | Banners, pulls, pity |
| **Lattice** | Permanent upgrade graph |
| **Archive** | Gallery, Codex, Bestiary, Constants, Theorems |

---

## 11. Enemies

- **Swarm points** (fast, many)
- **Sweepers**: rotating lines
- **Splitting polygons** (an n-gon breaks into (n−1)-gons when killed)
- **Shells**: polyhedra with faces you break one at a time
- **Phasers** (only if 4D stays): only hittable while crossing your 3-slice
- **Anomaly bosses**: Möbius strip, Klein bottle, torus knot, Lorenz attractor
- **Elites** roll random modifiers (shielded, splitting, hasted) and drop extra loot.

---

## 12. Tech plan

**TypeScript + WebGL2, packaged as an Android app with Capacitor.**

- **Vite + TypeScript**
- **three.js** for the scene + **custom GLSL** for glass, fields, and bloom
- **SolidJS** for UI: fine-grained updates for lots of live numbers
- **Glass layer:** DOM for layout and crisp text; a WebGL pass underneath draws the SDF union of all glass shapes and refracts the game buffer through them
- **Simulation:** fixed timestep, deterministic, seeded RNG, separate from rendering. The same sim runs headless for balance scripts and offline progress.
- **Content:** items, affixes, sets, Forms, and Constants live in typed data tables
- **Save:** IndexedDB, versioned with migrations, plus export/import of a save string (backup before reinstalls)

### One device makes this simpler
- **No low-end fallbacks.** The S25 Ultra (Snapdragon 8 Elite) has plenty of headroom, so glass can run at full resolution with heavy effects. **Target: 120 fps.**
- **During development, run it as a PWA.** Open the URL in Chrome on the phone and add it to the home screen. It updates instantly with each push, with no APK reinstalls.
- **For the final build, use Capacitor.** It wraps the same code as an APK with **native haptics** (Samsung's haptic engine through Android's HapticFeedback APIs feels much crisper than the web Vibration API's plain buzz). The APK gets built by **GitHub Actions** and you sideload it. No Android Studio needed on your end.
- **No store, no accounts.** Just sideload.
- **Dev menu:** since it's single-player, a hidden debug panel (give currency, jump Depth, force drops) speeds up testing a lot.

### Risks
- **Visual noise:** handled by the channel system and the hard cap (§8.1).
- **Power growth with no prestige:** new multiplier types per Layer/Lattice region, balanced in log space and checked with the headless sim.
- **Menus are the whole game:** if menu feel is weak, nothing else saves it. That's why M0 is about the glass UI.

---

## 13. Roadmap

| Milestone | Goal | Done when |
|---|---|---|
| **M0: Glass spike** | Prove the UI on the real device | A liquid-glass dock + sheet refracting an animated geometry field at 120 fps on the S25 Ultra (PWA) |
| **M1: Core loop** | Tower, enemies, projectiles, Depth, Flux, save/load | Can idle-farm with auto-Depth |
| **M2: Gear** | 6 slots/channels, drops, affixes, reforge, auto-salvage | Each slot's effect shows on the player and inherits to projectiles |
| **M3: Collections** | Red-dot system, Bestiary, Archive, Codex | Clearing dots feels great |
| **M4: Dimensions 0–3** | Forms, V/E/F stats, Rifts, Lattice | Can ascend to 3D |
| **M5: Depth content** | Echoes, Constants, synergies, sets | Systems complete. **Decide on 4D here.** |
| **M6: Ship to phone** | Offline progress, Capacitor APK via CI, haptics, audio, balance pass | Installed APK on the S25 Ultra |

---

## 14. Open questions
1. **RGB color system:** a core hook, or too much on top of channels + V/E/F? (§5)
2. **4D:** decide at M5 after seeing 3D on the device. (§3.2)
3. Portrait-only? (I'm assuming yes.)
