# Tileset Standards

**Status**: DRAFT — Awaiting art style decision
**Engine**: RPG Maker MZ
**Last Updated**: December 2025

---

## Overview

This document defines how tilesets must be created for RPG Maker MZ compatibility.

---

## RPG Maker MZ Specifications

### Tile Dimensions
- **Base tile**: 48x48 pixels (MZ standard)
- **Grid alignment**: All tiles must snap to 48px grid
- **Map unit**: 1 tile = 48x48px

### Tileset Image Sizes

| Type | Dimensions | Tiles | Purpose |
|------|------------|-------|---------|
| **A1** | 768x576 | Animated (water, waterfalls) | Auto-tiles with animation |
| **A2** | 768x576 | Ground auto-tiles | Grass, dirt, floors |
| **A3** | 768x384 | Wall auto-tiles | Building exteriors |
| **A4** | 768x720 | Wall tops | Upper walls, roofs |
| **A5** | 384x768 | Normal tiles | Regular single tiles |
| **B-E** | 768x768 | Normal tiles | Objects, decorations |

### File Format
- **Format**: PNG
- **Color depth**: 32-bit RGBA (transparency required)
- **No compression artifacts**

---

## Auto-Tile Format (A1-A4)

RPG Maker MZ uses a specific auto-tile format:

```
A2 Ground Auto-Tile Layout (per tile set):
┌──┬──┬──┬──┐
│░░│░▓│▓░│▓▓│  Row 1: Base patterns
├──┼──┼──┼──┤
│░▓│  │  │▓░│  Row 2: Edge patterns
├──┼──┼──┼──┤
│▓░│  │  │░▓│  Row 3: Edge patterns
├──┼──┼──┼──┤
│▓▓│▓░│░▓│░░│  Row 4: Corner patterns
└──┴──┴──┴──┘

Each "cell" is 48x48, total auto-tile block is 192x192
```

**Important**: Auto-tiles must follow MZ's exact layout or transitions break.

---

## Naming Convention

```
[region]_[tileset-type]_[description].png
```

**Examples**:
- `insect_A2_forest_ground.png`
- `mammal_B_cave_objects.png`
- `reptilian_A1_swamp_water.png`
- `avian_C_cloud_platforms.png`

**Regions**: `insect`, `mammal`, `reptilian`, `avian`, `shared`, `arena`
**Tileset Types**: `A1`, `A2`, `A3`, `A4`, `A5`, `B`, `C`, `D`, `E`

---

## Layers (MZ Standard)

| Layer | Purpose | Example |
|-------|---------|---------|
| **Ground (A)** | Base terrain | Grass, water, floors |
| **Objects (B-E)** | Decorations, obstacles | Trees, rocks, furniture |
| **Region** | Invisible gameplay zones | Encounter areas, triggers |
| **Shadow** | Auto-generated | Under walls/objects |

---

## Passability Settings

Set in Database > Tilesets:

| Symbol | Meaning | Use |
|--------|---------|-----|
| ○ | Passable | Open ground |
| × | Impassable | Walls, obstacles |
| ☆ | Star (above player) | Treetops, bridges |
| ◇ | Passable + trigger | Doors, stairs |

**Directional**: Can set per-direction (↑↓←→) for ledges.

---

## Color Palette by Region

**TBD** — Awaiting art style decision

Proposed direction:
- **Insect Region**: Forest greens (#2d5a27), earth browns (#8b6914), moss
- **Mammal Region**: Stone grays (#6b6b6b), mountain browns (#4a3728), snow whites
- **Reptilian Region**: Desert tans (#c4a35a), swamp greens (#3d5c3d), volcanic reds
- **Avian Region**: Sky blues (#87ceeb), cloud whites (#f0f0f0), sunset oranges

---

## Checklist Before Submission

- [ ] Correct dimensions for tileset type (A1-E)
- [ ] 48x48 tile grid alignment
- [ ] PNG format with transparency
- [ ] Follows naming convention
- [ ] Auto-tile layout correct (if A1-A4)
- [ ] Passability settings documented
- [ ] Color palette consistent with region
- [ ] No visible seams when tiled
- [ ] Tested in MZ editor

---

## Tools

- **Recommended**: Aseprite, Photoshop, GIMP
- **Templates**: Use MZ's default tilesets as layout reference
- **Testing**: Always import and test in actual MZ project

---

## Common Mistakes

1. **Wrong dimensions** — MZ is strict about tileset sizes
2. **Auto-tile layout wrong** — Causes broken transitions
3. **48x48 grid misalignment** — Tiles won't connect properly
4. **No transparency** — Background color shows through
5. **Inconsistent style** — Clashes with other region assets

---

## Resources

- RPG Maker MZ Help: Tileset configuration
- [Community templates on itch.io]
- Default RTP as reference (don't ship with it unless licensed)

---

*This document must be finalized before any tileset work begins.*
