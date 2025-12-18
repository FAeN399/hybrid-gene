# Hybrid Gene

**Real-time monster breeding and battle arena game.**

Breed. Train. Battle.

---

## Vision

A monster-raising game where creatures have opinions. Unlike turn-based competitors, Hybrid Gene features:

- **100% Real-Time Combat** — No menus, no turns. Position and timing matter.
- **Monster Autonomy** — Low INT = can't understand orders. Low Temperament = won't obey.
- **Generational Breeding** — G1 real animals → G2 hybrids → G3 mythological → G4 deity-tier secrets.
- **Action-Based Growth** — No XP. Stats grow from battle actions with diminishing returns.

---

## Species

| Species | Strength | Weakness | Trait |
|---------|----------|----------|-------|
| **Insect** | High AGI | Low INT | — |
| **Mammal** | High INT | Balanced | — |
| **Reptilian** | High END/STR | Low AGI | — |
| **Avian** | High AGI/INT | Low END | Flying (50% melee dodge, +20% ranged damage taken) |

---

## Project Structure

```
├── Hybrid-Gene/     # RPG Maker MZ game files
└── Gatekeep/        # Documentation & coordination
    ├── Standards/   # Asset specs (tilesets, sprites, plugins, database)
    ├── docs/        # GDD, Tech Spec, Demi.md
    ├── answers/     # Design questionnaire responses
    └── *.html       # Interactive tools (task board, task request)
```

## Documentation

| Document | Description |
|----------|-------------|
| [GDD](Gatekeep/docs/HybridGene-GDD.md) | Game Design Document |
| [Technical Spec](Gatekeep/docs/HybridGene-TechSpec.md) | Implementation details, data structures, systems |
| [Demi](Gatekeep/docs/HybridGene-Demi.md) | Living document — the soul of the project |
| [Task Board](Gatekeep/task-board.html) | Claim and track development tasks |

HTML versions available in `Gatekeep/docs/` for visual presentation.

---

## Core Systems

### Combat
- 1v1, 1v2, 2v2 real-time battles
- Player commands 2 monsters via controller
- Commands can be ignored based on monster INT + Temperament
- Green flash = obeyed, Red flash = ignored → Core AI takes over

### Breeding
- Same species + same generation → next generation
- Stats inherited via formula with variance
- Moves inherited if child can learn them
- Birthmarks (random) determine personality + stat growth modifiers

### Capture
- Weaken below 25% HP → tranquilize
- Carry back to base (half speed, no items)
- Wild monsters start with low temperament

---

## Inspirations

- **Digimon World 1** — Monster autonomy, breeding depth
- **Link to the Past** — Real-time combat feel

---

## Status

**Pre-Production** — Design phase complete. Implementation pending.

---

## Website

[arcsolaire.com](https://arcsolaire.com) — Crescent Sun

---

*The monster has opinions. That's the point.*
