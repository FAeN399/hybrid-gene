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

## Task 2: Sprite Implementation Planning

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Research sprite workflow for RPG Maker MZ
- Define art style direction (pixel art vs. hand-drawn)
- Evaluate asset sources (custom vs. commissions vs. generators)
- Test sprite sheet format with sample character
- Document animation frame requirements

### Deliverables
- [ ] Art style decision document
- [ ] Asset source strategy (create, commission, or mix)
- [ ] Sample sprite test (1 monster proof-of-concept)
- [ ] MZ sprite sheet format guide (dimensions, frames)
- [ ] Animation requirements per creature type
- [ ] Tool recommendations for sprite creation
- [ ] Create `Standards/Sprites.md` with finalized specs

### Skills Needed
- RPG Maker MZ sprite understanding
- Research / evaluation
- Basic art for testing concepts

---

## Task 3: Plugin Foundation Research

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Research existing MZ plugins for real-time combat
- Evaluate VisuStella vs. custom development
- Test basic plugin structure and MZ architecture
- Identify what's possible vs. what needs custom code

### Deliverables
- [ ] Plugin ecosystem evaluation (what exists, costs, licenses)
- [ ] VisuStella feasibility report (can it do real-time?)
- [ ] Sample plugin test (basic MZ plugin structure)
- [ ] Technical requirements doc for combat/AI/breeding
- [ ] Build vs. buy decision for each system
- [ ] Create `Standards/Plugins.md` with architecture notes

### Skills Needed
- JavaScript basics
- RPG Maker MZ plugin research
- Technical evaluation

---

## Task 4: Database Structure Planning

**Status**: OPEN
**Assigned**: —
**Support**: —

### Scope
- Research MZ database structure and limitations
- Define data schema for monsters, moves, items
- Plan stat ranges and formula foundations
- Create spreadsheet templates for future entry

### Deliverables
- [ ] MZ database capabilities doc (fields, limits, custom data)
- [ ] Stat range definitions (min/max for each stat)
- [ ] Base formula templates (damage, growth, inheritance)
- [ ] Spreadsheet template for monster entries
- [ ] Spreadsheet template for move entries
- [ ] ID allocation plan (see `ID-Register.md`)
- [ ] Create `Standards/Database.md` with schema specs

### Skills Needed
- RPG Maker MZ database familiarity
- Spreadsheet organization
- Basic game math understanding

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
