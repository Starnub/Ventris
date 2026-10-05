# Ventris — Handoff for a new chat

**Read this first, then `docs/DESIGN.md`.** If the two disagree, this file wins. It records what the user actually confirmed. The design doc also contains Claude's own proposals, and some of those were never reviewed.

Repo: `starnub/ventris`. All work so far is on branch `ccr-602ae7bf-5zmxnl`. **Stage: brainstorming only.** The user said "no implementation yet." Don't write game code until they ask.

---

## 1. Working with this user

- **Memory:** they say their memory is terrible. **Explain every term or system you bring up**, even ones discussed before. Never assume they remember something. The glossary at the top of DESIGN.md exists for this reason.
- **Tone:** casual, like a smart friend. No sycophancy, and be honest when something is weak. **No AI mannerisms** ("That's real", "It's not X, it's Y", "Let me flag that", etc.).
- **Numbering:** when they reply to a numbered list, keep their numbers. If you skip an item they already answered, say so ("3 and 4 you already answered").
- **Brainstorm style that works:** one topic at a time. Give **one clear recommendation plus at most one backup**, and check each idea against the rules for that topic before proposing it. They reject a lot, which is normal. Log every rejection.
- **What they consistently want:**
  - **Unique and fundamental:** an idea must change *how something works* in a way you can **see**. "+X% when Y" gets rejected.
  - **Clear and simple:** it has to read instantly on a phone, including on a 20-faced shape. Busy detail gets rejected.
  - **Abstract, geometric, glass and light.** Nothing organic (no resin, liquid, rubber).
  - No extra "combo effects" layered on top of things.
- **Claude's known failure modes in this project:** drifting from earlier decisions in long context (e.g. proposing opaque faces after "faces must stay see-through" was established), and adding things nobody asked for. Re-check the confirmed list below before proposing anything.
- **Process:** after each settled point, update `docs/DESIGN.md`, commit, and push to the branch. Attribution lines go at the end of commit messages, as the system specifies.

---

## 2. The game in one paragraph

**Ventris** is a single-player idle tower defense game for **Android, Samsung Galaxy S25 Ultra only**. It's a personal "forever game": no purchases, no online features, developed for as long as it stays fun. **You are the tower**: an abstract shape in a pitch-black void. It farms enemies continuously (no levels, no runs), and **everything is permanent: no prestige, no resets, no upkeep** (chores get automated). The visuals are pure black with **Apple Liquid Glass-style UI** that refracts the live game behind it, and everything is generated from math (no art assets). It has heavy RNG (drops, stat rolls, rerolls, pulls), lots of shallow systems you can 100%, and satisfying "red dot" clearing. **The menus are the gameplay.** Combat is fully automatic with no tap abilities. The UI should make people go "I've never seen UI like this."

---

## 3. Confirmed by the user

| Topic | Decision |
|---|---|
| Platform | Android, S25 Ultra only, portrait. Personal. No purchases. Offline single-player. |
| Core | Idle TD. You're the tower. Continuous farming deeper into **Depth**. No prestige/resets. No upkeep. |
| Interaction | Menus are the game. **No tap/active abilities.** |
| Look | Pitch black + liquid glass. Everything is abstract procedural geometry. |
| Gear visuals | Everything equipped shows on the player. Effects are **clear, distinct, not too many**, and fused into the shape rather than bolted on. |
| RNG | As much as possible: stat lines, rerolls, pulls. Rolling "perfect" stats. Outgrown gear goes into a **display** (the user's idea → the "Archive"). |
| Red dots | Only for actionable things. Each one clears in 2 taps or fewer. |
| Progression | New dimensions/Layers add **new kinds of multipliers**, not just bigger numbers. |
| Dimensions | **Finite: 0D → 1D → 2D → 3D.** No infinite n-D. **4D is parked** (decide much later). |
| Attacks (user's design) | Each dimension has its own attack. **0D:** a dot with a trail. **1D:** a laser that pierces in a straight line, then fades. **2D:** a pulse going outward *from the player* in the polygon's shape, hitting an area. **3D:** a faded clone of your polyhedron appears centered on the target and hits the area several times. **Items change both how the attack looks and what it does.** |
| Battlefield | **Enemies all come from one direction.** **The shape always rotates slowly.** A destroyed face lets enemy shots through when the rotation turns it toward the enemies. |
| Gear slots | The parts of the shape: **Vertex** (corners), **Weave** (edges), **Shell** (faces), **Cell** (interior). Each slot unlocks with the dimension that introduces that part. |
| Cell | **In.** A fractal lives inside the glass body and gains recursion depth as it levels. Details still to be designed. |
| Vertex traits | **Flare** (corners glint), **Comet** (corners leave light trails as the shape spins), **Beacon** (light travels corner to corner). All three **can run at the same time** (late unlock, "Harmonics"). **No extra combo effects.** |
| Weave traits | **Dotted** and **Double** confirmed. The third must read clearly and work with each of the other two separately. "Braided" was rejected. *Wavy* was proposed but never reviewed (see §4). |
| Shell = defense | Faces are for defense, not attack. |
| Shell: Facade | **All the faces merge into one large face** pointed at the enemies, acting as one shield with one shared health pool. The user's idea; confirmed. |
| Sets | Smaller sets (one piece per slot) are fine. **Set bonuses must change how something works, not add +X%.** |
| RGB | Damage types and resistances are **Red, Green, Blue** (replacing physical/magic). |
| Constants | Relics that **completely change your playstyle.** Must change a rule of the world, never just numbers. |
| Euler's five | **e, i, π, 1, 0** are in. Owning all five ("Euler's Identity", e^(iπ)+1=0) unlocks a second Constant slot. |
| π | Attacks circle you instead of flying outward. |
| 0 | You stop attacking. Your shape grows and erases whatever touches it. |
| e | Attacks start tiny and grow exponentially as they travel (weak up close, huge at range). |
| 1 | **The user's favorite.** All enemies in a wave share one health pool. |
| i | The first hit deals nothing and turns the enemy into a ghost. The second hit makes it real and deals the pair's damage *squared*. **Ghosts can still damage you.** Balance approach (square the damage relative to the current Depth's enemy HP) is in DESIGN.md §6.5 and wasn't objected to. |
| Constant bosses | Bosses every **100 Depth** ("Thresholds") guard the Constants. |
| Forever game | Two kinds of features: **modular** (fully independent, can be removed) and **integrated** (depends on, or is depended on by, other features). Keep a good balance. |
| Synergy Codex | **Removed.** But the user likes collections and wants that idea used for *something else*. |
| Lattice | The permanent upgrade tree (glowing node graph, bought with "Axioms"). The user said "neat"; details later. |

---

## 4. Open: where we stopped

### 4a. Shell (faces), in progress
Need **two more face traits** to go with **Facade**. Every trait must pass all of these:
1. **Stays see-through.** The Cell fractal must remain visible: nothing opaque, filled, or mirrored.
2. **Geometric, glass, or light themed.** Nothing organic.
3. **Readable on 20 small faces *and* on one merged Facade.** No fine detail.
4. **Changes a real property of the face**, different from the other traits' properties, so all three can stack.
5. **Defensive**, and not a number tweak.
6. **Works on a face attached to the body.** Without Facade, a face can't physically steer things away from the body.
7. **Feels like a fundamental change** that reads instantly.

**Rejected so far, with reasons. Don't re-propose these:**
- Hollow (hides other traits)
- Dense (hides fractal)
- Mirror (opaque, hides fractal)
- Prism, both versions (attack-only originally; later didn't read well and wasn't fundamental)
- Crackle (too busy)
- Exploded (not unique enough)
- Stained (a single merged face changing color doesn't work)
- Vessel (liquid waterline; didn't change a property of the face)
- Absorb (fill with light, then flash)
- Heartbeat (rhythmic shove)
- Phase (fade-in/out dodge)
- Amber and Elastic (organic)
- Refract (too complicated; an attached face can't bend things away)

**Unreviewed:** *Trap*. Shots get caught inside the glass as bouncing light streaks until they fade (total internal reflection). Don't assume it's good; it may fail rule 6 or 7.

### 4b. Agenda after Shell (in order)
1. **Weave third trait:** confirm or replace *Wavy* (edges become sine waves; the attack sweeps a wider band). It never got a response.
2. **Cell fractals:** the list, and what each does.
3. **Set bonuses**, held to the "changes how something works" bar.
4. **Collections:** what should be collected, now that the Codex is gone.
5. **Enemies + Layers:** the user is "iffy" on the current ideas; needs a fresh discussion. Remember that enemies come from one direction.
6. **Lattice** details.
7. Check: the 2D Pulse and the π Constant send attacks in all directions, but enemies only come from one. Does that waste too much?
8. Review the older systems the user never explicitly looked at (§5).
9. When the user says go: **M0 prototype**, the liquid-glass UI running on the S25 Ultra.

---

## 5. In DESIGN.md but proposed by Claude and never reviewed

Treat these as drafts. Raise them with the user rather than building on them as if they were decided.

- **"Any unlocked Form can be equipped"**, so ascending adds attack types rather than replacing them.
- **Enemy color = what it resists**, with mixed colors (yellow = R+G, etc.). The RGB *types* are confirmed; this rule isn't.
- **Digit leveling for Constants** (π: 3 → 3.1 → 3.14 …).
- Rarity names (Integer → Rational → Irrational → Transcendental → Imaginary → Complex), affix tiers, reroll actions, the four currencies (Flux, Shards, Prisms, Axioms), Rifts/pity numbers, Bestiary, Theorems, the Archive's bonus rules, UI tab list, the modular/integrated rules and backlog (§16), tech stack (TypeScript + WebGL2 + three.js + SolidJS + Capacitor), and the roadmap.
- **Harmonics unlock details** (socket count, how it's unlocked). The *concept* of all three traits running at once is confirmed; the mechanics aren't.
- The **Rejected-ideas log** for Constants is in DESIGN.md §6.4.
