# Game Design Kit (carried over from Ventris)

The generic, reusable parts of the Ventris plan, with everything specific to that game removed: no dimensions, no shape slots, no Constants, no RGB.

Each item is tagged with where it came from:
- **[You]**: you confirmed it in the Ventris chats.
- **[Proposed]**: Claude suggested it and you never reviewed it. Treat these as drafts.

---

## 1. Working together

- **[You]** Your memory is bad by your own account, so **explain every term every time**, even ones discussed before. Keep a glossary at the top of the design doc.
- **[You]** Casual tone, like a smart friend. No sycophancy, and no AI mannerisms.
- **[You]** When you reply to a numbered list, keep your numbers.
- **[You]** Brainstorm one topic at a time, with **one recommendation plus at most one backup**. Check each idea against that topic's rules before pitching it.
- **[You]** Log every rejected idea along with the reason, so it never gets pitched again.
- **[You]** After each settled point, update the design doc, commit, and push.
- **Lessons from Ventris:**
  - **Settle the foundations before the details.** Ventris went deep on details (face traits, relic math) before it had a power curve, a sense of pacing, or a combat model.
  - **Tag every decision in the doc** as confirmed, proposed, or open. Ventris's "Decisions" table mixed Claude's guesses in with your choices, and later chats treated those guesses as settled.
  - **Long chats drift.** Write a `HANDOFF.md` before a chat gets long, and start fresh.
  - **Avoid name clashes.** Ventris used the same word for two different things more than once (e.g. "Imaginary" was both a rarity and a relic; "Shells" was both an enemy type and a gear slot).

## 2. Design taste (what you consistently wanted)

- **[You]** **Unique and fundamental.** An upgrade has to change *how something works* in a way you can see. "+X% when Y" gets rejected.
- **[You]** **Clear and simple.** It has to read instantly on a phone screen. Busy detail gets rejected.
- **[You]** **No combo effects** layered on top of things that already work on their own.
- **[You]** **Abstract, geometric, glass and light.** Nothing organic. (This was Ventris's theme, but it was also clearly your taste.)
- **[You]** **Everything you equip shows on the player**, fused in rather than bolted on, and kept to a small number of effects.

## 3. Pillars

| Pillar | Meaning | |
|---|---|---|
| Permanent | No prestige and no resets. Progress never goes away. | [You] |
| Zero upkeep | No durability, stamina, energy, or repairs. Chores get automated or cut. | [You] |
| Menus are the gameplay | Decisions happen in menus, so they need to feel better than any menu you've used. No tap abilities. | [You] |
| Lots of RNG, all of it fun | Drops, stat rolls, rerolls, pulls. Bad luck gets softened, never punished. | [You] |
| Small things to finish | Many shallow systems you can 100%, each with its own red dots and completion moment. | [You] |
| Pure math visuals | Everything is generated geometry. No art assets. | [You] |
| Forever game | Personal project, no purchases, offline, developed for as long as it stays fun. | [You] |

## 4. UI / UX

### Look
- **[You]** **Pitch-black background** (true `#000` on OLED). The only light comes from the game.
- **[You]** **Apple Liquid Glass-style UI that refracts the live game behind it.** The goal: "I've never seen UI like this."
- **[Proposed]** What the glass does:
  - chromatic dispersion (rainbow fringing) at the panel rims
  - frosted blur that varies with the glass's thickness
  - a specular highlight that moves with the phone's gyroscope
  - **liquid merging**: neighboring panels blend into each other like droplets (smooth-min SDFs)
- **[Proposed]** When menus cover the game, keep a faint drifting field of geometry behind the glass, so the glass always has something to bend.

### Feel
- **[Proposed]** Spring physics on everything, and every gesture can be interrupted midway.
- **[Proposed]** Native haptics with distinct patterns for taps, rarity reveals, perfect rolls, and red-dot clears.
- **[Proposed]** Procedural audio in one musical key, e.g. kills play pentatonic notes.
- **[Proposed]** Menus open as bottom sheets over the live game, so you never leave it.
- **[Proposed]** A "while you were gone" glass card on return that you swipe to collect.
- **[Proposed]** An inspect view that lets you pinch-zoom and rotate the player.

### Red dots
- **[You]** A red dot only appears when there's something you can act on, and every dot clears in **2 taps or fewer**.
- **[Proposed]** Dots roll up the menu tree (tab → panel → card).
- **[Proposed]** Long-pressing a tab clears everything under it.
- **[Proposed]** Clearing a dot feels physical: a glass droplet pops with a tone and a haptic tick, and the pitch rises as you chain clears.

### Device: Samsung Galaxy S25 Ultra **[You]**
- **[Proposed]** Specs: 1440×3120, about 412×891 CSS px at 3.5× DPR, 120 Hz.
- **[Proposed]** Edge-to-edge layout with a safe area around the punch-hole camera.
- **[Proposed]** Main controls in the bottom third of the screen.
- **[You]** Portrait orientation.
- **[Proposed]** One device means no low-end fallbacks. The target is 120 fps.

## 5. RNG and loot systems

- **[You]** As much RNG as possible: stat lines, rerolls, pulls, and chasing "perfect" rolls.
- **[You]** Outgrown gear goes into a **display** instead of being deleted. Ventris called it the **Archive**.
- **[Proposed]** **Affixes**: each item has 1–6 stat lines. Each line has a tier (T1–T10) and a roll within that tier's range.
  - A **perfect line** is top tier with the max roll.
  - A **perfect item** has every line perfect and gets a permanent shimmer.
- **[Proposed]** Reroll menu:

| Action | Effect |
|---|---|
| Reforge | Reroll one line's value within its tier |
| Retier | Reroll one line's tier |
| Transmute | Swap one line for a different stat |
| Lock | Protect lines during a full reroll (extra cost per lock) |
| Full reroll | Reroll every unlocked line |

- **[Proposed]** Rolls spin like a slot machine and snap into place with a haptic tick. Perfect rolls get their own sound and flash.
- **[Proposed]** **Duplicates** turn into stars (★1–★5) on the copy you already own. Stars raise the roll ceilings and polish the item's visual effect.
- **[Proposed]** **Rarity changes the quality of an effect, not how many effects there are.**
- **[Proposed]** **Pulls** (gacha) with pity that's shown on screen and carries across banners. The currency is earned only by playing.
- **[Proposed]** **Archive bonus**: each displayed item gives a tiny permanent bonus (×3 if it's perfect), and full sets get a pedestal.
- **[You]** **Sets** are small (one piece per slot), and **set bonuses must change how something works**, not add +X%.

## 6. Collections and completion

- **[You]** You like collections. Ventris's main collection system (the Synergy Codex) got cut, but you wanted the idea reused somewhere.
- **[Proposed]** Every completion gives a small permanent bonus.
- **[Proposed]** Example collection systems:
  - **Bestiary**: kill milestones per enemy type (10 / 100 / 1k / 10k / 100k).
  - **Achievements as "proofs"**: Ventris called them Theorems.
  - **Set and perfection codexes**: find every piece, then find a perfect copy of every piece.
- **Lesson:** Ventris ended up with eight collection systems, which is probably too many. Pick a few.

## 7. Idle structure

- **[You]** Continuous farming, with no runs or levels.
- **[Proposed]** Auto-advance: you go deeper when you clear fast enough, and get pushed back a little when you fail. Nothing is lost and there's no fail screen.
- **[Proposed]** A lock that lets you farm a chosen zone.
- **[Proposed]** Offline progress pays your measured clear rate, with a generous cap.
- **[Proposed]** Automation:
  - auto-collect drops
  - auto-salvage by rarity and stat filters
  - auto-advance
  - loadout presets that switch by rule
  - auto-claim offline progress
  - auto-equip, off by default
- **[You]** Progression should add **new kinds of multipliers**, not just bigger numbers on the old ones.
- **Still unsolved in Ventris; settle these first next time:**
  - how you get stronger forever without prestige
  - how long each stage of the game lasts
  - what you actually decide in the menus once everything is automated

## 8. Feature structure for a forever game

- **[You]** Every feature is one of two types, and the mix stays roughly balanced:
  - **Modular**: fully independent and can be removed.
  - **Integrated**: depends on other features, or other features depend on it.
- **[Proposed]** Rules:
  - A **modular** feature depends only on the core, and nothing depends on it. It can be switched off in **Settings → Features**. Switching it off pauses it, and switching it back on resumes exactly where it left off.
  - An **integrated** feature declares its dependencies and can never depend on a modular feature.
- **[Proposed]** Every feature plugs into the core through the same contract:
  - stat contributions
  - event hooks (on kill, on hit, on wave, on return from offline…)
  - a red-dot provider
  - a UI entry (tab, card, or section)
  - its own versioned save section
  - data tables for its content
- **[Proposed]** The core never imports features.

## 9. Tech plan [all Proposed]

- **Stack**: TypeScript + Vite, three.js + custom GLSL (glass, bloom), SolidJS for UI, packaged with Capacitor.
- **Glass layer**: the DOM handles layout and crisp text. A WebGL pass underneath draws the glass shapes and refracts the game through them.
- **Simulation**: fixed timestep, deterministic, and seeded RNG, kept separate from rendering. The same sim runs headless for balance scripts and offline progress.
- **Content**: lives in typed data tables.
- **Save**: IndexedDB, versioned with migrations, plus export/import as a save string.
- **Development**: run it as a PWA on the phone, which updates with every push. Include a dev menu (give currency, jump ahead, force drops).
- **Release**: GitHub Actions builds an APK with native haptics, and you sideload it.
- **First milestone ("glass spike")**: before any gameplay, prove a liquid-glass dock and sheet refracting an animated background at 120 fps on the S25 Ultra. If the UI is the selling point, it's also the biggest risk.
