
# The Farmer Was Replaced
## Community Reference Documentation (Complete Edition)

> This document is a **complete, structured and community-oriented documentation**
> based entirely on the official wiki and in‑game behavior.
> It is intended to be the **single source of truth** for players, automation enthusiasts
> and competitive leaderboard runners.

---

## 1. About the Game

**The Farmer Was Replaced** is an automation and programming game where the player controls
a drone using a Python‑like language.  
The core objective is not farming itself, but **thinking in algorithms**, **automation**,
**performance**, and **scalability**.

The language is intentionally close to Python, but:
- Execution is **tick-based**
- Performance matters
- Some Python features behave differently

---

## 2. Execution Model (VERY IMPORTANT)

### 2.1 Ticks and Operations

- Every instruction consumes **ticks**
- 200 ticks ≈ one physical action (move, harvest, plant)
- 1 tick ≈ sensor or logic operation

> Side effects **happen immediately**, then the delay happens.

Example:
```python
harvest()  # harvest happens instantly, delay happens after
```

### 2.2 Speed & Power

- Speed upgrades reduce tick duration
- Sunflower **Power** doubles execution speed
- Power drains faster with higher speed upgrades

---

## 3. Language Fundamentals

### 3.1 Variables

- Dynamically typed
- Assigned with `=`
- No `global` keyword exists

Important difference from Python:
```python
x = 1

def f():
    x += 1  # creates a local x, does NOT modify global

f()
print(x)  # prints 1
```

### 3.2 Booleans

- `True`
- `False`

Used mainly in `if` and `while`.

---

## 4. Control Flow

### 4.1 while

Used for **continuous automation**.
Infinite loops are normal and expected.

```python
while True:
    if can_harvest():
        harvest()
```

### 4.2 if / elif / else

Conditional execution.
Used for:
- harvest safety
- ground checks
- unlock logic

```python
if get_ground_type() != Grounds.Soil:
    till()
```

### 4.3 for

Used when the number of iterations is known.

Most common use:
**systematic farm traversal**.

```python
for i in range(get_world_size()):
    move(North)
```

---

## 5. Movement System

### Directions
- North (up)
- South (down)
- East (right)
- West (left)

Movement wraps around farm edges.

```python
move(North)
```

`move()` returns:
- `True` if movement succeeded
- `False` if blocked (maze walls, tail, etc)

---

## 6. Systematic Farm Traversal

Canonical traversal pattern:

1. Move North until wrap
2. Move East
3. Repeat forever

```python
while True:
    for i in range(get_world_size()):
        move(North)
    move(East)
```

This pattern **never breaks** when the farm expands.

---

## 7. Ground Types

### Grassland
- Default ground
- Grass grows automatically

### Soil
- Created by `till()`
- Required for most crops

```python
if get_ground_type() != Grounds.Soil:
    till()
```

---

## 8. Plants (Entities)

### Grass
- Grows on grassland
- Harvested into Hay

### Bush
- Drops Wood
- Faster growth than trees

### Tree
- Drops more Wood
- Growth slows with nearby trees

### Carrots
- Requires soil
- Core early‑game currency

### Pumpkins
- Fast growth
- Used for advanced unlocks

### Sunflowers
- Produce Power
- Incorrect harvest destroys all

### Cactus
- Size‑based
- Requires sorting to harvest

### Hedge & Treasure
- Part of Maze system

### Dinosaur
- Snake‑like mechanics
- Harvest yields n² Bones

---

## 9. Harvesting Rules

- `harvest()` destroys non‑harvestable entities
- Always guard with `can_harvest()`

```python
if can_harvest():
    harvest()
```

---

## 10. Watering

- Water level: `0 → 1`
- Growth multiplier depends on water
- Water evaporates over time

```python
if get_water() < 0.5:
    use_item(Items.Water)
```

---

## 11. Fertilizer

- Instantly grows plants by 2 seconds
- Dries soil completely after use

```python
use_item(Items.Fertilizer)
```

---

## 12. Sensors (Senses Unlock)

Common sensors:
- get_pos_x()
- get_pos_y()
- get_world_size()
- get_entity_type()
- get_ground_type()
- get_water()
- num_items()
- get_time()
- get_tick_count()

Sensors cost **1 tick**.

---

## 13. Data Structures

### Lists
Ordered collections.

### Dictionaries
Key‑value storage.
Keys can be tuples.

### Sets
Unordered, unique values.

### Tuples
Immutable, indexable, unpackable.

```python
x, y = measure()
```

---

## 14. Functions

Functions allow abstraction and reuse.

```python
def harvest_if_ready():
    if can_harvest():
        harvest()
```

Calling a function directly costs **0 ticks**
(except the function body itself).

---

## 15. Mazes

- Created using `Items.Weird_Substance`
- Maze size depends on substance amount and upgrades
- Treasure yields maze_area gold

Key facts:
- No loops unless reused
- Walls block movement
- `move()` returns False when blocked

Recommended strategy:
**Wall following (left or right hand rule)**

---

## 16. Polyculture

Plants prefer a companion plant.

```python
companion = get_companion()
```

If planted correctly:
- Yield is multiplied (10x → 160x)

---

## 17. Cactus Sorting

Harvest spreads only if:
- All neighbors are grown
- Sizes are sorted:
  - North/East ≥ current
  - South/West ≤ current

Yield:
```text
n harvested → n² cactus
```

Sorting requires **adjacent swaps only**.

---

## 18. Dinosaurs

- Activated via Dinosaur Hat
- Snake‑like tail grows when moving
- Apples extend tail
- Tail blocks movement

Harvest:
```text
tail length n → n² bones
```

---

## 19. Unlock System

Key functions:
- unlock()
- get_cost()
- num_unlocked()

Automation depends on checking costs dynamically.

---

## 20. External Editor Support

- Code saved as `.py`
- `__builtins__.py` enables IntelliSense
- File Watcher enables hot reload

---

## 21. Debug & Benchmark

Tools:
- Step execution
- print()
- quick_print()
- get_tick_count()

Used for optimization and leaderboard runs.

---

## 22. Leaderboards

Categories:
- Fastest Reset
- Maze
- Dinosaur
- Resource‑specific

Runs require **2h simulated time minimum**.

---

## 23. Best Practices

- Always guard harvest
- Prefer clarity over cleverness
- Measure before optimizing
- Automate unlocks
- Design traversal first

---

## 24. Final Philosophy

This game rewards:
- Thinking in systems
- Incremental abstraction
- Performance awareness

> If your code works on a 3x3 farm,
> it should still work on a 100x100 farm.

---

Source:
https://thefarmerwasreplaced.wiki.gg/
