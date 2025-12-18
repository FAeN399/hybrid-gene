# Plugins - Technical Standards

**Status**: DRAFT
**Engine**: RPG Maker MZ
**Last Updated**: December 2025

---

## Core Plugin: MZ3D

| Property | Value |
|----------|-------|
| Name | MZ3D (Modified) |
| Author | CutieVirus |
| Cost | $25 |
| Owner | Drew (Dagyr) |
| Source | [cutievirus.itch.io/mz3d](https://cutievirus.itch.io/mz3d) |

### MZ3D Features
| Feature | Status |
|---------|--------|
| GLTF/GLB Import | Yes |
| Wall Culling | Yes |
| Camera Rotation | Yes |
| Dynamic Shadows | Yes |
| Point Lights | Yes |
| Directional Light | Yes |
| Weather Effects | Via MZ default |

### MZ3D Configuration

```javascript
// Plugin parameters (TBD after setup)
// Documented here after Drew configures
```

---

## Plugin Requirements

### Must Have
| Plugin | Purpose | Status |
|--------|---------|--------|
| MZ3D | 3D rendering | Owned |
| Real-time battle system | Combat | TBD |
| Monster AI | Autonomy | TBD |

### Nice to Have
| Plugin | Purpose | Status |
|--------|---------|--------|
| QoL improvements | UX | TBD |
| Save system enhancement | Data | TBD |

---

## Custom Plugins (Planned)

### Breeding System
- Parent stat inheritance
- Generation progression
- Birthmark assignment
- Cooldown management

### Monster AI
- Core AI behaviors (aggressive, defensive, supportive, evasive)
- Obedience calculation
- Command interpretation
- INT/Temperament checks

### Capture System
- Tranquilize mechanics
- Carry state
- Wake chance

### Growth System
- Action-based stat growth
- Diminishing returns formula
- Generation-based ceilings

---

## Plugin Load Order

```
1. Core (MZ default)
2. MZ3D
3. [Battle System - TBD]
4. [Monster AI - TBD]
5. [Breeding - TBD]
6. [Growth - TBD]
7. [Capture - TBD]
```

---

## File Structure

```
Hybrid-Gene/
└── js/
    └── plugins/
        ├── MZ3D.js
        ├── HG_Battle.js      (custom)
        ├── HG_MonsterAI.js   (custom)
        ├── HG_Breeding.js    (custom)
        ├── HG_Growth.js      (custom)
        └── HG_Capture.js     (custom)
```

---

## Resources

- [MZ3D Documentation](https://cutievirus.com/docs/mz3d/)
- [RPG Maker MZ Plugin Help](https://forums.rpgmakerweb.com)

---

*Drew (Dagyr) manages plugins. Contact for plugin questions.*

---

**TODO**: Document MZ3D configuration after setup. Define custom plugin specifications.
