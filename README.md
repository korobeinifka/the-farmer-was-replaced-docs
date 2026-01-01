
# The Farmer Was Replaced
## Complete Community Documentation

### Overview
The Farmer Was Replaced (TFWR) is an automation-focused game using a Python-like language.
Although the syntax resembles Python, execution is based on **ticks**, and performance is a core gameplay mechanic.

---

## Language Fundamentals

### Booleans
True and False are the only boolean literals.

### While
Used for continuous automation. Infinite loops are expected.

### If / Elif / Else
Conditional branching. `can_harvest()` is the primary early-game condition.

### For
Used when the iteration count is known. Essential for grid traversal.

---

## Movement System

Directions:
- North
- East
- South
- West

Movement wraps around the grid.

---

## Grid Traversal Patterns

Canonical traversal:
- Move North until wrap
- Move East
- Repeat forever

---

## Plants and Ground

### Ground Types
- Grassland
- Soil

### Core Plants
- Grass
- Bush
- Tree
- Carrot
- Pumpkin
- Sunflower
- Cactus

---

## Harvesting Rules

- `harvest()` destroys non-harvestable entities
- Always guard with `can_harvest()`

---

## Watering System

- Water level: 0–1
- Growth multiplier: 1 + water * 4
- Water evaporates over time

---

## Fertilizer

- Grows plants instantly by 2 seconds
- Dries soil completely afterward

---

## Sensors (Senses)

- get_pos_x / get_pos_y
- get_world_size
- get_entity_type
- get_ground_type
- get_water
- num_items
- get_time
- get_tick_count

---

## Data Structures

### Variables
Dynamic typing, Python-like semantics (with differences in scope).

### Lists, Dictionaries, Sets, Tuples
Behave mostly like Python, with reference semantics.

---

## Functions

User-defined functions enable reuse and abstraction.
Function calls have performance implications.

---

## Debugging Tools

- Breakpoints
- Step-by-step execution
- print() and quick_print()

---

## Performance Model

- Actions cost ~200 ticks
- Sensors cost ~1 tick
- Side effects happen at function start

Optimization is gameplay.

---

## Advanced Systems

### Cactus Sorting
Harvest cascades if sorted by size.

### Pumpkins
20% death chance. Mega-pumpkins yield cubic rewards.

### Sunflowers
Generate Power. Harvesting incorrectly destroys all.

### Trees
Growth slows with adjacent trees.

### Mazes
Generated with Weird Substance. Solvable via wall-following.

### Dinosaurs
Snake-like tail mechanics. Final harvest yields n² bones.

---

## Unlock System

- unlock()
- get_cost()
- num_unlocked()

Automation depends on programmatic unlocking.

---

## External Editor

- Files saved as .py
- __builtins__.py enables IntelliSense
- File Watcher applies live changes

---

## Best Practices

- Harvest only when ready
- Prefer clarity over cleverness
- Measure performance
- Automate everything

---

## End Goal

Automate → Optimize → Reset → Compete

Source:
https://thefarmerwasreplaced.wiki.gg/
