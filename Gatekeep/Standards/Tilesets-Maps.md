# Tilesets & Maps - Technical Standards

**Status**: ACTIVE
**Engine**: RPG Maker MZ + MZ3D Plugin
**Last Updated**: December 2025

---

## Tech Stack

| Layer | Tool | Purpose |
|-------|------|---------|
| **Game Engine** | RPG Maker MZ | Game logic, events, database |
| **3D Plugin** | MZ3D (modified) | 3D rendering, camera, lighting |
| **3D Modeling** | Crocotile 3D | Build 3D maps from 2D tiles |
| **Tile Creation** | Aseprite / AI | Create base tile textures |

---

## Pipeline

```
Tile Creation (AI/Hand-drawn)
        ↓
    .png (48x48 or 16x16)
        ↓
Crocotile 3D (build 3D environment)
        ↓
    .gltf export
        ↓
MZ3D Plugin (import & render)
        ↓
RPG Maker MZ (game)
```

---

## Tile Specifications

### Base Tiles
| Property | Value |
|----------|-------|
| Size | 48x48px (MZ standard) or 16x16px (Crocotile native) |
| Format | PNG (32-bit RGBA) |
| Transparency | Required |
| Seamless | Required for terrain |

### Crocotile 3D Settings
| Property | Value |
|----------|-------|
| Unit Scale | 1 unit = 16 pixels |
| Export Format | .gltf / .glb |
| Texture Mode | Pixel-perfect (no filtering) |

---

## MZ3D Capabilities

| Feature | Supported |
|---------|-----------|
| GLTF Import | Yes |
| Wall Culling | Yes |
| Camera Rotation | Yes |
| Dynamic Shadows | Yes |
| Point Lights | Yes |
| Directional Light | Yes |
| Weather Effects | Via MZ default |

---

## AI Tile Generation

### Midjourney
```
pixel art grass tile, 16x16, seamless, top-down RPG --tile --v 4
```
- Use `--tile` for seamless
- V4 better for pixel art than V5
- Clean up in Aseprite before use

### Stable Diffusion
- Enable "Tiling" checkbox
- Free / local alternative
- More setup required

---

## File Naming Convention

```
[region]_[type]_[description].png
```

**Examples:**
- `insect_ground_grass.png`
- `mammal_wall_stone.png`
- `reptilian_floor_sand.png`
- `avian_platform_cloud.png`

**Regions:** `insect`, `mammal`, `reptilian`, `avian`, `shared`, `arena`

---

## Crocotile 3D Export Settings

```
Format: GLTF (.gltf or .glb)
Texture: Embedded or External
Scale: 1.0
Y-Up: Yes (MZ3D default)
```

---

## Folder Structure

```
Hybrid-Gene/
├── img/
│   ├── tilesets/          # Raw 2D tiles for reference
│   └── parallaxes/        # Pre-rendered backgrounds (if needed)
├── models/
│   ├── maps/              # .gltf map files
│   └── objects/           # .gltf props/decorations
└── data/
    └── MapInfos.json      # MZ map data
```

---

## Tools & Costs

| Tool | Cost | Owner |
|------|------|-------|
| Crocotile 3D | $30 | Drew |
| MZ3D Plugin | $25 | Drew |
| RPG Maker MZ | $80 | — |
| Aseprite | $20 | — |
| Midjourney | $10/mo | — |

---

## Workflow Checklist

- [ ] Create/generate base tiles (48x48 or 16x16)
- [ ] Import tileset into Crocotile 3D
- [ ] Build 3D map geometry
- [ ] Set up lighting in scene
- [ ] Export as .gltf
- [ ] Import into MZ3D
- [ ] Configure collisions in RPG Maker MZ
- [ ] Add events and triggers
- [ ] Test in-game

---

## Resources

- [Crocotile 3D](https://crocotile3d.com/) - $30
- [Crocotile Documentation](https://www.crocotile3d.com/howto.html)
- [MZ3D Plugin](https://cutievirus.itch.io/mz3d) - $25
- [MZ3D Documentation](https://cutievirus.com/docs/mz3d/)
- [Midjourney Tile Parameter](https://docs.midjourney.com/docs/tile)

---

*Drew (Dagyr) manages 3D pipeline. Contact for Crocotile/MZ3D questions.*
