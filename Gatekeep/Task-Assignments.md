# Task Assignments

Active development roles and assignments.

---

## Assignment Key

| Status | Meaning |
|--------|---------|
| `OPEN` | No one assigned, ready to claim |
| `ASSIGNED` | Has owner, work in progress |
| `PAUSED` | Owner unavailable, can be picked up |

---

## Task 1: Tileset Implementation Planning

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Research tileset workflow for RPG Maker MZ
- Evaluate asset sources (custom art vs. asset packs vs. RTP)
- Define pipeline from concept to in-engine
- Test auto-tile format with sample tiles
- Document process for future asset creation

### Deliverables
- [ ] Workflow document (how tiles go from idea to MZ)
- [ ] Asset source decision (create, buy, or mix)
- [ ] Sample tileset test (1 region proof-of-concept)
- [ ] Tool recommendations (Aseprite, Photoshop, etc.)
- [ ] Template files for each tileset type (A1-E)
- [ ] Update `Standards/Tilesets.md` with finalized process

### Skills Needed
- RPG Maker MZ tileset understanding
- Research / evaluation
- Basic pixel art for testing

---

## Task 2: Sprite Collections

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Monster sprites (100+ creatures across 4 generations)
- Character sprites (player, NPCs, arena masters)
- Animation frames for combat actions
- Battler graphics for combat system

### Deliverables
- [ ] G1 monster sprites (16 real animals, 4 per species)
- [ ] G2 monster sprites (exotic hybrids)
- [ ] G3 monster sprites (mythological)
- [ ] G4 monster sprites (6+ deity-tier secrets)
- [ ] Player/NPC character sheets
- [ ] Attack/ability animations
- [ ] Status effect visual indicators

### Skills Needed
- Pixel art / sprite animation
- Consistency across 100+ designs
- Understanding of MZ sprite sheet format

---

## Task 3: Plugin Development

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Real-time combat system (not turn-based)
- Monster AI with obedience/autonomy
- Breeding system mechanics
- Custom UI for stance commands

### Deliverables
- [ ] Real-time battle engine plugin
- [ ] Monster AI behavior system
- [ ] Obedience calculation (INT + Temperament)
- [ ] Command input handling (D-Pad stances, L1/R1 moves)
- [ ] Breeding eligibility and inheritance logic
- [ ] Growth/decay stat system
- [ ] 5-party member support (MZ default is 4)

### Skills Needed
- JavaScript (MZ plugin format)
- RPG Maker MZ plugin architecture
- VisuStella compatibility (if using their base)
- Game AI patterns

### Notes
May use VisuStella ATB/CTB as base, or build custom from scratch.

---

## Task 4: Database Population

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Define all monsters, moves, items in MZ database
- Balance stats, damage formulas, costs
- Configure birthmarks and their modifiers
- Set up species traits and available moves

### Deliverables
- [ ] 100+ monster entries with stats
- [ ] 4 species definitions with base stats/traits
- [ ] 100+ birthmark configurations
- [ ] 100+ move definitions (4 categories)
- [ ] Item database (battle items, food, materials)
- [ ] Damage/healing formulas balanced
- [ ] Arena bracket configurations

### Skills Needed
- RPG Maker MZ database editor
- Game balance understanding
- Spreadsheet work for planning
- Attention to ID conventions (see `ID-Register.md`)

---

## How to Claim a Task

1. Check the task's required standards doc exists in `Standards/`
2. If standards missing, submit request via `task-request.html`
3. Update this file with your name and change status to `ASSIGNED`
4. Coordinate with Support person if assigned
5. Check `Tasks.md` for any blockers

---

## Notes

- RPG Maker MZ handles solo development well
- 1 person per task is fine; 2 for larger scopes
- Plugin Development may need dedicated focus
- All tasks should reference `ID-Register.md` for numbering

---

*Last updated: December 2025*
