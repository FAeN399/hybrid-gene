# Hybrid Gene
## Game Design Document

**Version**: 1.0
**Last Updated**: December 2024
**Status**: Pre-Production

---

## 1. Executive Summary

### Vision Statement
Hybrid Gene is a real-time monster breeding and battle arena game where players raise, breed, and command semi-autonomous creatures. Unlike traditional monster-catching games with turn-based combat, Hybrid Gene features fluid real-time battles where monsters have their own intelligence and may choose to ignore commands based on their stats and temperament.

### Core Fantasy
**Breed. Train. Battle.**

The player is a commander and coach—not a direct controller. Monsters are partners with opinions, not tools that execute orders perfectly. Victory comes from understanding your creatures, building trust through proper care, and strategic breeding across generations.

### Key Differentiators
- **100% Real-Time Combat**: No menus, no turns. Position, timing, and reaction matter.
- **Monster Autonomy**: Creatures have hidden obedience stats. Low intelligence means they can't understand orders. Low temperament means they won't obey. Commands can be ignored.
- **Generational Breeding**: Four generations of monsters, from real animals (G1) to mythological creatures (G3) to secret deity-tier hybrids (G4).
- **Action-Based Growth**: No experience points or levels. Stats grow through battle actions with diminishing returns.

### Target Experience
- **Playtime**: 40-60 hours to become Grand Champion
- **Tone**: Strategic but fast-paced, rewarding both careful planning and quick reflexes
- **Audience**: Players who enjoy monster-raising games but want more active combat engagement

### Reference Games
- **Digimon World 1**: Monster autonomy, breeding depth, raising mechanics
- **The Legend of Zelda: A Link to the Past**: Real-time combat feel, fluid movement

---

## 2. Core Loop

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│   EXPLORE ──► CAPTURE ──► BREED ──► TRAIN ──► BATTLE   │
│      ▲                                           │      │
│      │                                           │      │
│      │           ◄── ARENA ◄── REWARDS ◄─────────┘      │
│      │                  │                               │
│      └──────────────────┘                               │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

1. **Explore**: Traverse the island's four themed regions
2. **Capture**: Weaken wild monsters, tranquilize, and carry them home
3. **Breed**: Combine same-generation monsters to create next-gen offspring
4. **Train**: Battle to grow stats through actions (not XP)
5. **Battle**: Real-time combat controlling two monsters simultaneously
6. **Arena**: Compete in ranked tournaments to progress
7. **Rewards**: Earn currency, items, and area access
8. **Repeat**: Unlock new regions, discover stronger monsters

---

## 3. Monsters

### 3.1 Species

Four species inhabit the island, each with distinct stat profiles and behaviors.

| Species | STR | INT | AGI | END | Aggression | Special Trait |
|---------|-----|-----|-----|-----|------------|---------------|
| **Insect** | Medium | Low | High | Medium | Medium | — |
| **Mammal** | Medium | High | Medium | Medium | Medium | — |
| **Reptilian** | High | Low | Low | High | High | — |
| **Avian** | Low | High | High | Low | Low | Flying |

**Flying Trait**: 50% chance to dodge melee attacks, but takes 20% extra damage from ranged attacks.

### 3.2 Generations

Monsters evolve through breeding across four generations:

| Generation | Description | Count | Visual Style |
|------------|-------------|-------|--------------|
| **G1** | Real animals | 16 (4 per species) | Realistic creatures |
| **G2** | Exotic hybrids | Variable | Mixed features, unusual colors |
| **G3** | Mythological | ~100 total | Fantasy creatures, legendary beasts |
| **G4** | Deity-tier | 6+ | Divine/cosmic beings |

**Breeding Rules**:
- Same species + Same generation → Next generation offspring
- G3 cross-species breeding → Secret G4 creatures (e.g., Avian G3 + Reptile G3 = Quetzalcoatl)

### 3.3 Birthmarks

Every monster is born with a random birthmark that permanently shapes its development:

- **Personality**: Affects flavor text and minor behaviors
- **Core AI Archetype**: Determines autonomous behavior when commands are ignored
  - Aggressive: Target nearest enemy, spam attacks
  - Defensive: Maintain distance, counter-attack only
  - Supportive: Prioritize ally buffs and heals
  - Evasive: Avoid damage, flee when HP is low
- **Stat Modifiers**: -20% to +20% growth rate per stat

Birthmarks cannot be changed. Breeding for ideal birthmarks is part of the strategic depth.

---

## 4. Stats & Growth

### 4.1 Core Stats

| Stat | Abbreviation | Affects | Grows By |
|------|--------------|---------|----------|
| **Strength** | STR | HP, Physical Power, Max Energy | Attacking |
| **Intelligence** | INT | Special Power, Obedience, Move Learning | Using abilities |
| **Agility** | AGI | Movement Speed, Reaction Time | Moving around |
| **Endurance** | END | HP, Energy Regeneration Rate | Taking damage |

### 4.2 Derived Stats

Calculated from core stats using formulas:

- **HP** = BaseHP + (STR × 2) + (END × 3)
- **Max Energy** = BaseEnergy + (STR × 1.5)
- **Energy Regen** = BaseRegen + (END × 0.5)
- **Movement Speed** = BaseSpeed + (AGI × 0.1)
- **Obedience** = BaseObedience + (INT × 0.4) + (Temperament × 0.6)

### 4.3 Growth System

**No Levels**: Stats grow directly from battle actions, not experience points.

**Growth Decay**: As stats increase, growth rate decreases. This creates natural soft caps.

- **Formula**: `GrowthMultiplier = 1 / (1 + CurrentStat / DecayThreshold)`
- **Decay Thresholds by Generation**:
  - G1: 50 (hits ceiling fastest)
  - G2: 75
  - G3: 100
  - G4: 150 (highest potential)

**Implication**: Lower generation monsters can still be competitive through extended training, but higher generations have significantly higher ceilings.

### 4.4 Birthmark Impact

Birthmark modifiers apply to all stat gains:

```
ActualGain = BaseGain × BirthmarkModifier × GrowthMultiplier
```

A +20% STR birthmark on a G4 monster creates the highest possible strength potential.

---

## 5. Breeding System

### 5.1 Eligibility

- Both parents must be the same species
- Both parents must be the same generation
- Breeding cooldown applies after each session (duration TBD)
- Age requirement may apply (TBD)

### 5.2 Offspring Generation

- G1 + G1 → G2
- G2 + G2 → G3
- G3 + G3 → G3 (same generation, but potentially better stats)
- G3 (Species A) + G3 (Species B) → G4 (specific combinations only)

### 5.3 Inheritance

**Stats**:
```
ChildStat = ((Parent1Stat + Parent2Stat) / 2) × (0.8 + Random(0.4))
```
Starting stats determine initial growth rate decay position.

**Moves**:
- Child inherits moves that both parents know AND the child's species can learn
- Enables strategic move inheritance chains

**Birthmarks**:
- Randomly generated fresh for each offspring
- Cannot be inherited or influenced

### 5.4 Strategic Depth

Players can:
- Breed for optimal birthmarks across many generations
- Stack parent stats to give offspring higher starting points
- Inherit specific move combinations
- Create G4 secrets through cross-species G3 breeding

---

## 6. Combat System

### 6.1 Battle Format

- **Style**: 100% real-time, no pausing for commands
- **Modes**: 1v1, 1v2, 2v2
- **Player Control**: Commands two monsters simultaneously
- **Camera**: Top-down or 2.5D with slight depth
- **End Conditions**: All enemy monsters reach 0 HP, or player flees to another screen

### 6.2 Monster Autonomy

The core differentiator. Monsters are not perfectly obedient.

**Obedience Calculation**:
```
Obedience = BaseObedience + (INT × 0.4) + (Temperament × 0.6)
```

**Command Resolution**:
1. Player issues command
2. System rolls against monster's Obedience stat
3. If roll succeeds: Monster executes command
4. If roll fails: Monster follows Core AI behavior instead

**Visual Feedback**:
- Green flash: Command accepted
- Red flash: Command ignored

**Low INT Monsters**: Literally cannot understand complex commands. Simple creatures act on instinct.

**Low Temperament Monsters**: Understand but refuse. Wild captures start with low temperament. Proper care increases it.

### 6.3 Controls

| Input | Action |
|-------|--------|
| **D-Pad** | Stance orders (Aggressive / Defensive / Supportive / Passive) |
| **L1** | Select Monster 1, hold for move commands |
| **R1** | Select Monster 2, hold for move commands |
| **A/B/X/Y** | Execute moves (while holding L1 or R1) |
| **L1+L2** | Advanced options for Monster 1 |
| **R1+R2** | Advanced options for Monster 2 |
| **L2** | Use item on Monster 1 |
| **R2** | Use item on Monster 2 |

**Command Cooldown**: 0.5 seconds per monster between commands

### 6.4 Moves

**Slot Structure**: 8 total moves per monster
- 4 Basic attacks: Low energy cost, low cooldown
- 4 Special attacks: High energy cost, high cooldown

**Categories**:
- Physical (STR-based damage)
- Magic/Special (INT-based damage)
- Buff (enhance self or ally)
- Debuff (weaken enemy)
- Heal (restore HP)
- AoE/Multi-hit (area damage)

**Energy System**:
- Monsters have an energy pool (Max Energy from STR)
- Energy regenerates over time (rate from END)
- Regeneration slows as battle duration increases
- Strategic resource management required

**Learning Moves**:
1. Inherited from parents at birth
2. Reaching stat thresholds
3. Watching another monster use a learnable move (INT check)

### 6.5 Status Effects

| Effect | Description |
|--------|-------------|
| **Poison/DoT** | Damage over time |
| **Stun/Freeze** | Cannot act temporarily |
| **Slow** | Reduced movement speed |
| **Blind** | Reduced accuracy |
| **Burn** | Damage over time + reduced attack |

### 6.6 Combat Feel

- **Hit Stagger**: Brief interrupt animation on damage
- **Screen Shake**: Impact feedback on heavy hits
- **Sound Design**: Distinct sounds for attacks, hits, abilities
- **Visual Effects**: Particles, flashes, trails

---

## 7. Capture & Taming

### 7.1 Tranquilization

Wild monsters can be captured through tranquilization:

1. Weaken monster below 25% HP
2. Use tranquilizer item
3. Success rate scales with remaining HP:
   - 25% HP: 50% success
   - 5% HP or less: 100% success

**Risk**: If battle continues after tranq, monster has 10% chance per turn to wake up

### 7.2 Carrying

Once tranquilized:
- Player must physically carry monster back to base
- Movement speed reduced by 50%
- Cannot use items in battle while carrying
- If player's monsters are KO'd, the carried monster is lost

### 7.3 Wild Temperament

Captured monsters start with low temperament:
- They understand commands but often refuse
- Proper care (feeding, rest, gentle treatment) increases temperament
- High temperament = more obedient

### 7.4 Legendary Encounters

Each region contains a secret area with:
- One G4 legendary (not capturable)
- One G3 legendary (capturable)
- The G3 provides a hint for breeding that G4

---

## 8. World

### 8.1 Island Structure

The game takes place on an island divided into four themed regions:

| Region | Theme | Primary Species | Unlock Condition |
|--------|-------|-----------------|------------------|
| **Starting Region** | Forest/Meadow | Insect | — |
| **Region 2** | Mountains/Caves | Mammal | Rank B in Region 1 Arena |
| **Region 3** | Swamps/Desert | Reptilian | Rank B in Region 2 Arena |
| **Region 4** | Sky/Peaks | Avian | Rank B in Region 3 Arena |

**Shortcut**: Achieving Rank S in any arena allows skipping directly to Region 4.

### 8.2 Region Contents

Each region contains:
- ~20 screens of explorable wilderness
- Wild monsters to battle and capture
- Caves and structures with rare loot
- Boss encounters with high-generation monsters
- One arena for ranked competition
- NPCs and story elements

### 8.3 Player Base

- Starting capacity: 6 monsters
- Upgradable to 20 maximum
- NPCs can move in (shops, services)
- Enhances monster happiness and growth

---

## 9. Arena System

### 9.1 Structure

Each region has one arena with:
- **Bracket Tournaments**: Determine rank (D through S)
- **Ladder**: Persistent ranking of all competitors

### 9.2 Ranks

| Rank | Requirement | Benefit |
|------|-------------|---------|
| D | Entry level | — |
| C | Win D tournament | — |
| B | Win C tournament | Unlock next region |
| A | Win B tournament | — |
| S | Win A tournament | Skip directly to final region |

### 9.3 Rules

- **No Weight Classes**: Any monster can compete at any rank
- Bring G4 to D-rank if desired (for speedrunning or challenge)
- NPC competitors appear on the ladder
- Players can challenge ranked NPCs outside tournaments

### 9.4 Rewards

- Currency (Gold)
- Items and ingredients
- Food for growth buffs
- Area access
- Possibly: Monsters (as tournament prizes)

---

## 10. Economy

### 10.1 Currency

**Gold** (name TBD)

### 10.2 Sources

- Arena victories (scales with rank)
- Wild monster drops
- Selling items and ingredients
- Quest completion (if implemented)

### 10.3 Sinks

| Category | Examples |
|----------|----------|
| **Battle Items** | Heals, buffs, tranquilizers |
| **Food/Growth** | Temporary growth rate boosts |
| **Base Upgrades** | Monster capacity, facilities |
| **Cosmetics** | TBD |

---

## 11. Scope & Priorities

### 11.1 Must Have (v1.0)

1. **Breeding System**: Core generational mechanics, stat inheritance
2. **Combat**: Real-time battles with autonomous monster AI
3. **Arena**: Ranked tournaments with progression

### 11.2 Should Have

- Four complete regions with distinct theming
- 100+ monsters across generations
- Full capture and taming loop
- Base management (basic)

### 11.3 Cut First (If Needed)

1. Base building (complex upgrades)
2. Item crafting system
3. Food creation system

### 11.4 To Be Determined

- [ ] Monster lifespans / permanent death
- [ ] Day/night cycle
- [ ] Damage type system (elemental weaknesses)
- [ ] Crafting depth and balance
- [ ] Multiplayer functionality
- [ ] Currency name

---

## 12. Appendix

### 12.1 G1 Starter Roster (16 Total)

**Insect** (4):
- TBD real insects

**Mammal** (4):
- TBD real mammals

**Reptilian** (4):
- TBD real reptiles

**Avian** (4):
- TBD real birds

### 12.2 G4 Secret Creatures

| G4 Monster | Breeding Combination |
|------------|---------------------|
| Quetzalcoatl | Avian G3 + Reptile G3 |
| TBD | TBD |
| TBD | TBD |
| TBD | TBD |
| TBD | TBD |
| TBD | TBD |

### 12.3 Birthmark List

TBD - Full list of possible birthmarks with stat modifiers and Core AI assignments.

---

*Document End*
