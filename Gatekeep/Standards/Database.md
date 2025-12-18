# Database - Technical Standards

**Status**: DRAFT
**Engine**: RPG Maker MZ
**Last Updated**: December 2025

---

## Overview

This document defines the data structure standards for monsters, moves, items, and game systems in Hybrid Gene.

---

## Data Structures

### Monster

```javascript
{
  id: Number,
  name: String,
  species: "insect" | "mammal" | "reptilian" | "avian",
  generation: 1 | 2 | 3 | 4,

  birthmark: {
    id: Number,
    personality: String,
    coreAI: "aggressive" | "defensive" | "supportive" | "evasive",
    statModifiers: {
      str: Number,  // -0.2 to +0.2
      int: Number,
      agi: Number,
      end: Number
    }
  },

  stats: {
    str: Number,
    int: Number,
    agi: Number,
    end: Number
  },

  derivedStats: {
    hp: Number,
    maxHp: Number,
    energy: Number,
    maxEnergy: Number,
    energyRegen: Number,
    moveSpeed: Number
  },

  moves: [MoveId, MoveId, MoveId, MoveId,  // basic
          MoveId, MoveId, MoveId, MoveId], // special

  temperament: Number,  // 0-100
  obedience: Number,    // hidden, calculated

  parents: [MonsterId, MonsterId] | null
}
```

### Species

```javascript
{
  id: Number,
  name: String,
  baseStats: {
    str: Number,
    int: Number,
    agi: Number,
    end: Number
  },
  aggressionLevel: Number,  // affects default AI
  traits: [String],         // e.g., "flying"
  availableMoves: [MoveId]
}
```

### Move

```javascript
{
  id: Number,
  name: String,
  category: "physical" | "magic" | "buff" | "debuff" | "heal" | "aoe",
  energyCost: Number,
  cooldown: Number,     // seconds
  damage: Number,       // base damage multiplier
  effects: [EffectId],
  range: Number,        // units
  aoe: Number | null    // radius if applicable
}
```

### Birthmark

```javascript
{
  id: Number,
  name: String,
  personality: String,
  coreAI: "aggressive" | "defensive" | "supportive" | "evasive",
  statModifiers: {
    str: Number,
    int: Number,
    agi: Number,
    end: Number
  }
}
```

---

## Species Data

| ID | Name | STR | INT | AGI | END | Trait |
|----|------|-----|-----|-----|-----|-------|
| 1 | Insect | Med | Low | High | Med | — |
| 2 | Mammal | Med | High | Med | Med | — |
| 3 | Reptilian | High | Low | Low | High | — |
| 4 | Avian | Low | High | High | Low | Flying |

### Avian: Flying Trait
- 50% melee attack dodge chance
- +20% ranged damage taken

---

## Generation Roster

| Gen | Count | Type | Example |
|-----|-------|------|---------|
| G1 | 16 | Real animals | Beetle, Wolf, Lizard, Hawk |
| G2 | ~30 | Exotic hybrids | TBD |
| G3 | ~50 | Mythological | TBD |
| G4 | 6+ | Deity-tier secrets | Cross-species only |

---

## Formulas

### Obedience
```
obedience = baseObedience + (INT * 0.4) + (Temperament * 0.6)
```

### Stat Inheritance (Breeding)
```
childStat = (parent1.stat + parent2.stat) / 2 * (0.8 + random(0.4))
```

### Stat Growth (Action-based)
```
gain = baseGain * birthmarkModifier * decayMultiplier
decayMultiplier = 1 / (1 + stat / decayThreshold)
```

### Decay Thresholds by Generation
| Gen | Threshold |
|-----|-----------|
| G1 | 50 |
| G2 | 75 |
| G3 | 100 |
| G4 | 150 |

---

## RPG Maker MZ Database Mapping

| MZ Tab | Hybrid Gene Use |
|--------|-----------------|
| Actors | Monster templates |
| Classes | Species definitions |
| Skills | Moves |
| Items | Battle items, capture items |
| Weapons | — |
| Armors | — |
| Enemies | Wild monster encounters |
| States | Status effects |
| Animations | Attack/effect visuals |
| Common Events | Game systems |

---

## File Structure

```
Hybrid-Gene/
└── data/
    ├── Actors.json       # Monster templates
    ├── Classes.json      # Species
    ├── Skills.json       # Moves
    ├── Items.json        # Items
    ├── Enemies.json      # Wild monsters
    ├── States.json       # Status effects
    └── System.json       # Game config
```

---

## Naming Conventions

### Database Entries
```
[TYPE]_[SPECIES]_[GEN]_[NAME]
```

**Examples:**
- `MON_INSECT_G1_BEETLE`
- `MON_MAMMAL_G2_WOLFCAT`
- `MOVE_PHYSICAL_BITE`
- `MOVE_MAGIC_FIREBALL`

---

**TODO**: Define complete monster roster. Create move list. Document status effects.
