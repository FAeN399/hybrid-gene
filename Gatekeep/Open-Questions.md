# Open Questions

Decisions pending resolution.

---

## Format

```
### [QUESTION]
**Status**: Open / Decided / Deferred
**Priority**: High / Medium / Low
**Options**:
1. Option A - pros/cons
2. Option B - pros/cons
**Decision**: (when resolved)
**Date**: (when decided)
```

---

## Design Decisions

### Permanent Death
**Status**: Open
**Priority**: Medium
**Options**:
1. **Yes** - Creates emotional stakes, encourages careful play, matches Digimon World 1
2. **No** - Less frustrating, more casual-friendly, players can save-scum anyway
3. **Optional Hardcore Mode** - Best of both, but splits playerbase/testing

**Decision**:
**Date**:

---

### Damage Type System
**Status**: Open
**Priority**: Medium
**Options**:
1. **Add elemental types** - More depth, but risks Pokemon rock-paper-scissors
2. **Keep typeless** - Simpler, focuses on stats/strategy, original design intent
3. **Soft types** - Minor modifiers (10-20%) instead of hard counters

**Decision**:
**Date**:

---

### Multiplayer
**Status**: Open
**Priority**: Low (post-v1)
**Options**:
1. **Local only** - Simpler, no server costs
2. **Online PvP** - Natural fit for arena, requires balance pass
3. **Async battles** - Upload team, fight AI version of other players
4. **None** - Focus on single-player excellence

**Decision**:
**Date**:

---

### Monster Lifespans
**Status**: Open
**Priority**: Medium
**Options**:
1. **Age and die naturally** - Like Digimon World 1, creates attachment cycle
2. **Immortal** - No pressure, can invest indefinitely
3. **Retire system** - Choose to retire for bonuses, not forced

**Decision**:
**Date**:

---

### Day/Night Cycle
**Status**: Open
**Priority**: Low
**Options**:
1. **Aesthetic only** - Visual variety, no gameplay impact
2. **Spawn changes** - Different monsters at different times
3. **Behavior changes** - Nocturnal species more aggressive at night
4. **None** - Keep simple

**Decision**:
**Date**:

---

### Currency Name
**Status**: Open
**Priority**: Low
**Options**:
1. "Gold" - Generic, universal understanding
2. "Genes" - Thematic, ties to breeding
3. "Marks" - Connects to birthmarks
4. [Custom name TBD]

**Decision**:
**Date**:

---

## Technical Decisions

### Engine/Framework
**Status**: DECIDED
**Priority**: High
**Options**:
1. Godot - Free, 2D strong, GDScript or C#
2. Unity - Industry standard, C#, asset store
3. Custom - Full control, more work
4. **RPG Maker MZ** - Fast prototyping, plugin ecosystem

**Decision**: RPG Maker MZ
**Date**: December 2025
**Notes**: Real-time combat will require plugins (VisuStella or custom). See Gemini's workflow doc for team collaboration setup.

---

### Art Style
**Status**: Open
**Priority**: High
**Options**:
1. **Pixel art** - Nostalgic, achievable solo, clear readability
2. **Hand-drawn 2D** - Unique, requires artist
3. **3D low-poly** - Modern, harder to animate 100+ monsters

**Decision**:
**Date**:

---

### Platform Targets
**Status**: Open
**Priority**: Medium
**Options**:
1. **PC first** - Easiest development, controller support
2. **Mobile first** - Larger market, touch controls challenge
3. **Console** - Certification overhead, but fits genre

**Decision**:
**Date**:

---

## Resolved

<!-- Move decided questions here -->

---

*Last reviewed: December 2025*
