# Visual Style References v0.1

## Purpose

This document records historical game-style lessons that can guide the asset bible for **Maze: Pixel to 4K**. The goal is not to copy any one game, but to extract production principles from classic maze, dungeon, and room-based adventure design.

## Reference Principle

Use references as structural lessons:

- how many assets are needed
- how assets repeat
- how rooms and corridors are built
- how enemies are made readable
- how rewards and doors communicate progression

Do not copy direct sprites, names, maps, characters, logos, or protected visual designs.

## Classic Lessons

### Atari-style Adventure lineage

Useful lesson:

> A maze game can feel complete with very few assets if the rules are strong.

Takeaways:

- room-to-room structure can create exploration without large art sets
- keys, doors, simple enemies, and treasures are enough for a first prototype
- symbol clarity matters more than illustration detail

Production implication:

- prioritize `key`, `door`, `wall`, `floor`, and `enemy` readability first

### Arcade maze lineage

Useful lesson:

> One strong maze language can support endless repetition.

Takeaways:

- wall/floor contrast must be instant
- enemy silhouettes need to be readable under pressure
- pickups should be tiny but unmistakable
- simple movement rules can create high tension

Production implication:

- do not over-detail the floor
- make monsters visually distinct by silhouette, not by tiny costume detail

### Early dungeon crawler lineage

Useful lesson:

> Dungeon atmosphere can be created from a small set of repeated walls, floors, doors, and props.

Takeaways:

- repeated stone corridors are acceptable if pacing, mapping, and danger are strong
- torches, doors, stairs, and wall variants add enough environmental texture
- monsters can be introduced as discrete encounter icons or sprites

Production implication:

- first batch should be mostly reusable dungeon modules
- avoid making too many bespoke room illustrations

### Action-adventure room lineage

Useful lesson:

> Rooms are puzzles built from tiles.

Takeaways:

- one room can be defined by tile arrangement plus one mechanic
- a door, switch, key, trap, or enemy can define the room identity
- visual feedback must connect player action to world change

Production implication:

- `lever`, `pressure_plate`, `door`, and `trap` assets are as important as treasure assets

### Roguelike lineage

Useful lesson:

> Systemic variety can outperform asset quantity.

Takeaways:

- procedural layouts require strict tile grammar
- readable symbols are better than overproduced art
- enemy ecology and item logic matter more than many unique images

Production implication:

- maintain `data/assets.json` as the source of truth
- every asset should have category, role, reuse level, and priority

### Dark fantasy action RPG lineage

Useful lesson:

> Rich dungeons are assembled from modular kits.

Takeaways:

- walls, doors, floor trims, pillars, lighting, and prop clusters create atmosphere
- the same assets can feel different when arranged differently
- stronger enemies and bosses should appear only after environment identity is stable

Production implication:

- boss production comes after the tile set, not before it

## Style Direction for This Project

The first asset direction should be:

```text
pixel-first dark fantasy dungeon
serious and mysterious
classic tabletop fantasy atmosphere
ancient ruin + dungeon + synthesis relic logic
top-down orthographic readability
low saturation
strong silhouette
high reuse
```

## What to Avoid

Avoid these directions for the baseline:

- bright mobile idle-game fantasy
- generic anime RPG icon set
- modern cyberpunk neon dungeon
- photorealistic stone textures
- ornate illustrations that cannot be reused as tiles
- one-off scene paintings
- direct imitation of famous franchise symbols or characters

## Approved First-Batch Mood Keywords

Use these words consistently in prompts:

- modular
- dungeon
- old stone
- ancient ruin
- restrained palette
- readable silhouette
- top-down
- tile-based
- classic fantasy
- mythic medieval
- mysterious
- not whimsical
- no text
- no watermark

## Reference Outcome

The asset bible should lead toward a production system where:

1. A small tile set builds many mazes.
2. A few interactions create many room types.
3. Enemy ecology grows gradually.
4. Bosses are rare and meaningful.
5. Every generated asset has a stable ID and a defined gameplay role.
