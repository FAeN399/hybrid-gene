# Sprites - Technical Standards

**Status**: DRAFT
**Engine**: RPG Maker MZ + MZ3D Plugin
**Last Updated**: December 2025

---

## Overview

This document will define standards for monster sprites, character sprites, and animations for Hybrid Gene.

---

## Pending Decisions

| Decision | Options | Notes |
|----------|---------|-------|
| Sprite style | Pixel art / Hand-drawn / AI-assisted | — |
| Sheet format | Standard MZ / Custom | MZ3D may allow 3D models |
| Animation frames | 4 / 6 / 8 per direction | — |
| Monster display | 2D sprite overlay / 3D model | — |

---

## Placeholder Specs

### Character Sprites (if 2D)
| Property | Value |
|----------|-------|
| Size | 48x48px per frame (MZ standard) |
| Directions | 4 (down, left, right, up) |
| Frames | 3 per direction |
| Format | PNG (32-bit RGBA) |

### Monster Sprites (TBD)
| Property | Value |
|----------|-------|
| Size | TBD |
| Animation | TBD |
| Format | PNG or 3D model |

---

## File Naming Convention

```
[species]_[generation]_[name]_[state].png
```

**Examples:**
- `insect_g1_beetle_idle.png`
- `mammal_g2_wolfcat_attack.png`
- `reptilian_g3_drake_ko.png`

**Species:** `insect`, `mammal`, `reptilian`, `avian`
**Generations:** `g1`, `g2`, `g3`, `g4`
**States:** `idle`, `attack`, `hit`, `ko`, `special`

---

## Folder Structure

```
Hybrid-Gene/
├── img/
│   ├── characters/        # Player, NPCs
│   ├── enemies/           # Wild monster displays
│   ├── sv_actors/         # Side-view battle sprites (if used)
│   └── sv_enemies/        # Side-view enemy sprites (if used)
└── models/
    └── monsters/          # .gltf monster models (if 3D)
```

---

## Tools

| Tool | Cost | Purpose |
|------|------|---------|
| Aseprite | $20 | Pixel art, animation |
| AI (Midjourney/SD) | Varies | Base sprite generation |
| Blender | Free | 3D models (if needed) |

---

## Resources

- [RPG Maker MZ Sprite Standards](https://forums.rpgmakerweb.com)
- [Aseprite](https://www.aseprite.org/)

---

*Bear (Brian) manages sprite assets. Contact for sprite questions.*

---

**TODO**: Complete this document after sprite approach is decided.
