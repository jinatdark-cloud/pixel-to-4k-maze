# Dungeon Tile Rules v0.1

## Purpose

This document defines how reusable dungeon assets should fit together in **Maze: Pixel to 4K**. It exists so the project can avoid producing too many one-off images and instead build a durable tile vocabulary.

## Design Principle

The Maze should be built like a kit.

A good asset is not judged by how impressive it looks alone. It is judged by whether it can be reused across many rooms, corridors, and generated layouts without breaking visual consistency.

## Canonical Unit

The current demo uses:

```text
TILE = 40
```

For design purposes, this means:

| Unit | Meaning |
|---|---|
| 1×1 tile | one wall, floor, pickup, small prop, or small enemy space |
| 2×2 tiles | large prop or small boss |
| 3×3 tiles | large boss, portal room centerpiece, major altar |
| corridor width | 1 tile minimum in the current prototype |
| room block | built from repeated 1×1 tiles |

## Tile Categories

### 1. Floor tiles

Floor tiles are walkable by default.

They must:

- read clearly as empty space
- avoid strong outlines that make them look blocked
- support pickups, traps, and monsters placed above them
- remain visually quieter than walls

First families:

- `floor_stone`
- `floor_dirt`
- `floor_moss`

### 2. Wall tiles

Wall tiles are non-walkable by default.

They must:

- read clearly as obstacles
- have stronger mass than floors
- not contain unnecessary internal detail
- support straight corridor generation

First families:

- `wall_stone`
- `wall_brick`
- `wall_ruin`
- `wall_dungeon`

### 3. Corner tiles

Corners solve the visual problem of corridors feeling too square or too raw.

They should be used when the generator can identify wall adjacency patterns:

- inner corner
- outer corner
- broken corner
- ruin corner

In the current demo, they may be deferred until the renderer supports adjacency-aware tile selection.

### 4. Doors

Doors are route gates.

Rules:

- a door occupies one tile
- closed door blocks movement
- open door allows movement or ends the current objective
- door type should imply access level

First door types:

| ID | Use |
|---|---|
| `door_wood_01` | shallow/basic routes |
| `door_iron_01` | stronger locked route |
| `door_magic_01` | Access Tier or Weave-locked route |

### 5. Mechanisms and traps

Mechanisms communicate cause and effect.

Core interactions:

| Asset | State A | State B |
|---|---|---|
| lever | off | on |
| pressure plate | raised | pressed |
| spike trap | hidden/inactive | raised/active |
| portal | dormant | active |
| altar | inactive | activated |

The renderer should eventually support state-specific sprites.

### 6. Treasures and pickups

Pickups must remain readable at small size. They should not become miniature illustrations.

Rules:

- no text
- no complex heraldry
- one strong silhouette
- high contrast against floor
- consistent shadow/outline style

### 7. Monsters

Small monsters should occupy 1×1 tile in the first playable version. They should have:

- strong silhouette
- one readable facing direction first
- optional 4-direction animation later
- restrained detail

First ecology:

| Tier | Monsters |
|---|---|
| Low | giant rat, cave bat |
| Baseline combat | skeleton, goblin |
| Mid | orc, giant spider |

### 8. Bosses

Bosses should not be produced before base tiles work.

First boss footprints:

| Boss | Footprint |
|---|---|
| Minotaur-like maze guardian | 2×2 |
| Lich-like archivist | 2×2 |
| Ancient wyrm | 3×3 |

Do not make bosses too large until the camera and room system support them.

## Adjacency-Aware Wall Rendering

The future renderer should choose wall/corner visuals based on neighboring tiles.

Example:

```text
if tile is wall:
  check north/south/east/west neighbors
  choose straight wall, corner, endcap, or solid block variant
```

This allows one maze grid to look more natural without requiring hand-made full-room images.

## Room Construction Rules

### Basic corridor

```text
wall wall wall
floor floor floor
wall wall wall
```

### Small locked room

Minimum components:

- floor tiles
- wall tiles
- one door
- one treasure or mechanism
- optional torch or pillar

### Puzzle room

Minimum components:

- one blocked door
- one pressure plate or lever
- one visual signal that links cause and effect
- one reward or route change

### Boss room

Minimum components:

- entrance gate
- arena floor
- boundary wall
- visual centerpiece
- boss footprint
- reward or access unlock

## Reuse Ratio Rule

For every unique asset, create at least three reusable assets first.

Good ratio:

```text
3 reusable tiles : 1 unique prop
5 reusable tiles : 1 boss
```

Bad ratio:

```text
1 wall : 30 treasures : 20 bosses
```

## First Implementation Recommendation

The current demo should evolve in this order:

1. Replace hardcoded wall and floor colors with tile families.
2. Add `door_wood_01` and `key_bronze`.
3. Add `chest_small` as a reward after the exit.
4. Add `pressure_plate_01` and `spike_trap_01`.
5. Add one low-tier monster only after the player can read the environment clearly.

## Future 2.5D / 4K Upgrade Rule

Every asset should be able to evolve across resolution layers:

| Layer | Asset Interpretation |
|---|---|
| Pixel | simple tile/sprite |
| 8-bit | clearer outline, limited palette |
| 16-bit | richer tile detail |
| 2.5D | isometric wall/floor modules |
| HD | high-resolution painted or modeled asset |
| 4K | refined, high-detail version preserving original silhouette |

The silhouette should remain recognizable across all layers.
