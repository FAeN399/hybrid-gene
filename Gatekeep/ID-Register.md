# ID Register

Master allocation of numerical IDs to prevent collisions.

---

## Monster IDs

| Range | Owner | Purpose |
|-------|-------|---------|
| 001-016 | Core | G1 Starters (4 per species) |
| 017-050 | Core | G2 Monsters |
| 051-100 | Core | G3 Monsters |
| 101-110 | Core | G4 Secret Monsters |
| 900-999 | Debug | Test monsters (never ship) |

---

## Species IDs

| ID | Species |
|----|---------|
| 1 | Insect |
| 2 | Mammal |
| 3 | Reptilian |
| 4 | Avian |

---

## Move IDs

| Range | Category |
|-------|----------|
| 001-100 | Physical |
| 101-200 | Magic/Special |
| 201-250 | Buff |
| 251-300 | Debuff |
| 301-350 | Heal |
| 351-400 | AoE |
| 900-999 | Debug |

---

## Item IDs

| Range | Type |
|-------|------|
| 001-050 | Consumables (healing) |
| 051-100 | Consumables (buffs) |
| 101-150 | Capture items |
| 151-200 | Key items |
| 201-250 | Ingredients |
| 900-999 | Debug |

---

## Birthmark IDs

| Range | Core AI |
|-------|---------|
| 001-025 | Aggressive |
| 026-050 | Defensive |
| 051-075 | Supportive |
| 076-100 | Evasive |

---

## Map/Region IDs

| Range | Region |
|-------|--------|
| 001-020 | Insect Region (Starting) |
| 021-040 | Mammal Region |
| 041-060 | Reptilian Region |
| 061-080 | Avian Region |
| 081-090 | Arena Maps |
| 091-100 | Special/Cutscene |

---

## Variable IDs (if applicable)

| Range | Owner | Purpose |
|-------|-------|---------|
| 0001-0100 | System | Core game state |
| 0101-0300 | Combat | Battle mechanics |
| 0301-0500 | Breeding | Genetics system |
| 0501-0700 | World | Region/progression |
| 0701-0900 | Economy | Currency/inventory |
| 0901-1000 | Debug | Testing (never ship) |

---

## Rules

1. **Never reuse IDs** - Even if deleted, ID is burned
2. **Reserve 900+ for debug** - Strip before release
3. **Log all allocations** - Update this file immediately
4. **Gatekeeper approval required** - For new range requests

---

*Last updated: December 2024*
