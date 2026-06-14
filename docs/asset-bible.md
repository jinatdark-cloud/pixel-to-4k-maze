# Asset Bible v0.1 — First Modular Dungeon Batch

## Purpose

This document defines the first reusable asset system for **Maze: Pixel to 4K**. It translates the current world premise into a production-ready asset plan: start with repeatable dungeon building blocks, then expand into unique treasures, monsters, and bosses only after the base tile vocabulary is stable.

The goal is to prevent AI asset production from becoming a pile of unrelated images. Every visual asset should belong to a reusable family, have a stable ID, and support procedural maze construction.

## Canon Alignment

The existing project documents define the Maze as the foundation of civilization, not a side dungeon. The first demo already uses a canvas maze with walls, floors, a key, a door, and a player sprite. The first asset batch therefore focuses on assets that can immediately replace or extend those current primitive shapes.

Core production assumptions:

- **The Maze** is built from reusable spatial units.
- **Synthesis** and **Access Tiers** require readable interactive props such as keys, doors, levers, pressure plates, altars, and portals.
- **Expeditions** require strong environmental legibility: walls, floors, doors, hazards, pickups, and enemies must be understandable at small size.
- The visual system should support a long upgrade path from pixel-scale presentation to 8-bit, 16-bit, 2.5D, HD, and 4K interpretations.

## Creative Boundary

The baseline setting should stay within classic tabletop fantasy and mythic medieval high fantasy:

- stone corridors
- old ruins
- dungeons
- sealed doors
- keys and relics
- goblins, skeletons, bats, rats, spiders, orcs
- bosses such as a minotaur-like maze guardian, an undead archivist, and an ancient wyrm

Important IP rule:

> The game may evoke the feeling of classic tabletop fantasy, mythic medieval literature, and old dungeon crawlers, but it must not reproduce named characters, factions, symbols, emblems, maps, monsters with protected trade dress, or proprietary designs from any specific franchise.

Use the influence as a genre constraint, not as direct copying.

## Production Philosophy

### 1. Build with bricks before painting scenes

The correct unit of production is not “a dungeon illustration.” The correct unit is:

- wall tile
- floor tile
- corner tile
- door tile
- trap tile
- pickup prop
- enemy sprite
- boss footprint

This allows a small number of assets to generate many rooms and corridors.

### 2. Prefer reusable families over unique one-off images

A unique treasure or boss is allowed only when the base system is already stable. In Phase 1, the asset ratio should be roughly:

| Asset Type | Target Share | Reason |
|---|---:|---|
| Reusable environment tiles | 45–55% | Highest return for maze generation |
| Interactive props | 20–25% | Needed for gameplay logic |
| Pickups and treasures | 10–15% | Needed for progression feedback |
| Monsters | 10–15% | Needed for pressure |
| Bosses | 5% or less | Expensive, low reuse |

### 3. Every asset must have a gameplay role

Do not create decorative assets unless they help with:

- navigation
- readability
- progression
- risk signaling
- faction/world tone
- synthesis or access logic

## First Batch Summary

The first production batch contains **54 assets**:

| Family | Count | Purpose |
|---|---:|---|
| Walls | 8 | Core maze boundaries |
| Floors | 6 | Walkable tile vocabulary |
| Corners | 4 | Modular wall connection |
| Doors | 3 | Access and route gating |
| Pillars | 4 | Room structure and obstacles |
| Lights | 5 | Visibility and atmosphere |
| Mechanisms / hazards | 7 | Puzzle and danger language |
| Treasures / pickups | 8 | Reward and progression feedback |
| Monsters | 6 | First enemy ecology |
| Bosses | 3 | Long-term signature encounters |

## Priority System

| Priority | Meaning |
|---|---|
| P1 | Needed for the next playable prototype or asset replacement pass |
| P2 | Useful after the first tile replacement pass |
| P3 | Signature content; do later after base vocabulary is stable |

The current Phase 1 prototype should prioritize P1 assets:

- wall tiles
- floor tiles
- corners
- doors
- keys
- chests
- pressure plates
- levers
- spike trap
- small pickup gems

Monsters and bosses should be visually planned now, but implemented after the environment asset language is stable.

## Visual Rules

### Pixel-first baseline

The demo currently works in a pixel-like canvas style. The first art pass should keep assets readable at **40×40 px per tile**.

Baseline requirements:

- simple silhouette
- clear contrast between wall and floor
- no tiny decorative noise
- no text embedded in images
- no photographic texture
- no painterly background
- no perspective conflict with the current top-down grid

### Palette

Recommended first-pass palette:

| Use | Color Family |
|---|---|
| Background | black / near-black |
| Walls | charcoal, dark gray, stone gray |
| Floors | black, deep gray, muted brown |
| Wood | dark brown, aged brown |
| Metal | dull iron, muted silver |
| Moss / damp age | muted green only |
| Fire / candlelight | restrained amber |
| Arcane / Weave elements | controlled blue or cyan |
| Rare warning color | restrained red only for special pickups or danger |

Avoid excessive saturation. This project should feel serious, old, and mysterious, not candy-colored.

## Asset ID Rules

Use stable lowercase IDs:

```text
family_descriptor_variant
```

Examples:

```text
wall_stone_01
floor_moss_02
door_magic_01
pressure_plate_01
monster_skeleton
boss_minotaur
```

Rules:

- Do not rename an asset ID once it is referenced by code.
- Visual variants should increment the final number.
- Gameplay variants should use a semantic descriptor.
- Boss IDs should remain stable even if the art changes.

## AI Generation Prompt Template

Use this template for image generation after this asset table is accepted.

```text
Create a modular game asset for Maze: Pixel to 4K.

Asset ID: {asset_id}
Asset name: {asset_name}
Asset family: {family}
Gameplay role: {gameplay_role}
Production layer: {production_layer}
Tile footprint: {tile_size}

Style constraints:
- pixel-first fantasy dungeon asset
- classic tabletop fantasy atmosphere
- mythic medieval dungeon tone
- dark stone, old ruins, restrained palette
- readable at 40x40 px in the current canvas demo
- orthographic top-down view for the pixel demo
- clear silhouette
- transparent background
- no text, no watermark, no UI frame
- do not copy named characters, symbols, emblems, or proprietary franchise designs

Prompt focus:
{generation_prompt_focus}
```

## Animation Guidance

For Phase 1, do not animate everything.

Animate only:

- player direction
- door open/close
- torch/fire flicker
- pressure plate pressed/unpressed
- spike trap inactive/active
- portal pulse
- key/chest sparkle if needed

Use 2-frame or 4-frame sprite sheets first. Avoid complex animation until the base tile vocabulary is stable.

## Implementation Path

1. Keep the current canvas demo as the mechanical testbed.
2. Add asset IDs and metadata through `data/assets.json`.
3. Replace the current hardcoded wall/floor/key/door drawings one family at a time.
4. Test legibility at the existing 40 px tile size.
5. Only then generate higher-resolution versions.

## Next Asset Work

Recommended next tasks:

1. Generate only the P1 wall/floor/door/key/chest assets.
2. Add a simple asset loader to the demo.
3. Replace hardcoded colors with asset metadata.
4. Add trap and lever mechanics.
5. Add the first low-tier monster after traversal readability is stable.
