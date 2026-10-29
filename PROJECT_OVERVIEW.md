# Project Overview — "Your First 2D Game With Godot 4 (GDQuest)"

## Engine & Config
- **Engine**: Godot 4.6 (Forward Plus renderer, gl_compatibility backend)
- **Resolution**: 1920x1080, viewport stretch mode
- **Main Scene**: `res://survivors_game.tscn`
- **Language**: GDScript

## Genre
Top-down survival shooter — player moves with WASD, auto-fires at nearby slime mobs that chase the player. When health reaches zero, game over screen appears and the tree pauses.

---

## Scene Hierarchy (Main: `survivors_game.tscn`)

```
Game (Node2D)                          ← game.gd — spawner + game-over logic
├── Timer                              ← spawns mobs every 0.3s on random path positions
├── Player (CharacterBody2D)           ← player.tscn / player.gd
│   ├── HappyBoo (AnimatedSprite2D)    ← character sprite with walk/idle animations
│   ├── CollisionShape2D               ← rectangle 66x38
│   ├── Camera2D                       ← follows player
│   ├── Gun (Area2D)                   ← gun.tscn / gun.gd — auto-aim + auto-fire
│   │   ├── CollisionShape2D           ← circle r=987 detection radius
│   │   ├── WeaponPivot (Marker2D)     ← pivot for weapon rotation
│   │   │   ├── Pistol (Sprite2D)      ← pistol sprite
│   │   │   └── ShootingPoint (Marker2D) ← bullet spawn origin
│   │   └── Timer                      ← fires every 0.353s
│   ├── HurtBox (Area2D)               ← detects overlapping mobs, applies damage
│   └── HealthBar (ProgressBar)        ← visual health display above player
├── Path2D → PathFollow2D              ← mob spawn path (pentagonal loop around arena)
├── GameOver (CanvasLayer)             ← hidden until death; shows "Game Over" label + dark overlay
└── PineTree x10                       ← decorative scenery (trees/pine_tree.tscn)
```

---

## Scripts Summary

### `game.gd` — Game Manager / Spawner
- **Extends**: `Node2D`
- **Responsibilities**: Spawn mobs at random positions along a PathFollow2D, handle game-over state
- **Key Functions**:
  - `spawn_mob()` — instantiates `mob.tscn` at a random point on the path
  - `_on_timer_timeout()` — triggers spawn (every 0.3s)
  - `_on_player_health_depleted()` — shows GameOver UI, pauses tree

### `player.gd` — Player Controller
- **Extends**: `CharacterBody2D`
- **Responsibilities**: Movement (WASD via input actions), animation state, damage from overlapping mobs
- **Signals**: `health_depleted` — emitted when health ≤ 0
- **Key Variables**:
  - `health = 100.0`
  - `SPEED = 600` px/s
  - `DAMAGE_RATE = 6.0` per overlapping mob per second
- **Input Actions**: `move_left`, `move_right`, `move_up`, `move_down` (A/D/W/S)

### `mob.gd` — Enemy AI
- **Extends**: `CharacterBody2D`
- **Responsibilities**: Chase player, take damage, spawn death effect on kill
- **Key Variables**:
  - `speed = randf_range(200, 300)` (random per mob)
  - `health = 3` (takes 3 bullets to kill)
- **Signals**: `died` (defined but not currently connected)
- **Key Functions**:
  - `_physics_process()` — moves toward player via `direction_to()`
  - `take_damage()` — plays hurt animation, decrements health, spawns smoke explosion on death

### `gun.gd` — Auto-Aim Weapon
- **Extends**: `Area2D`
- **Responsibilities**: Detect nearest enemy in range (r=987), rotate toward it, fire bullets
- **Key Functions**:
  - `_process()` — finds closest overlapping body, calls `look_at()` to aim
  - `shoot()` — instantiates bullet at ShootingPoint with matching transform
  - `_on_timer_timeout()` — triggers shoot (every 0.353s)

### `bullet_2d.gd` — Projectile
- **Extends**: `Area2D`
- **Responsibilities**: Move forward in facing direction, self-destruct on range expiry or body collision
- **Key Variables**:
  - `SPEED = 1000` px/s
  - `RANGE = 1200` px max travel distance
- **Key Functions**:
  - `_physics_process()` — moves along rotated RIGHT vector, destroys if past range
  - `_on_body_entered(body)` — calls `body.take_damage()` if method exists, then self-destructs

### `smoke_explosion/smoke_explosion.gd` — Death Effect
- **Extends**: `Node2D`
- **Responsibilities**: Play explosion animation with randomized shader offset, auto-remove on finish

---

## Collision Layers
| Layer | Purpose |
|-------|---------|
| 1 (default) | Player body / Gun detection area |
| 2 ("player") | Mob collision layer — mobs are on this layer; player HurtBox and Gun mask against it |

- **Player CollisionShape2D**: default layer, detects nothing special
- **HurtBox (Area2D)**: mask=2 (detects mobs), layer=0
- **Gun (Area2D)**: mask=2 (detects mobs for aiming), layer=0
- **Mob CollisionShape2D**: layer=2

---

## Assets Structure
```
characters/
├── happy_boo/         ← player character sprite + animations
└── slime/             ← enemy character sprite + animations
pistol/
├── pistol.png         ← weapon sprite
├── projectile.png     ← bullet sprite
├── impact/            ← muzzle impact effects
└── muzzle_flash/      ← muzzle flash effects
smoke_explosion/       ← death particle effect (shader-based)
trees/
└── pine_tree.tscn     ← decorative tree scene
addons/
└── colorpicker_presets/  ← editor plugin
```

---

## Game Flow
1. Game starts → Timer spawns mobs every 0.3s at random positions on a pentagonal path around the arena
2. Each mob chases the player at random speed (200-300 px/s)
3. Gun auto-detects nearest mob in range (987px radius), aims, and fires every 0.353s
4. Bullets travel at 1000 px/s up to 1200px range; hitting a mob calls `take_damage()`
5. Mobs take 3 hits to die → spawn smoke explosion effect → queue_free
6. If mobs overlap the player's HurtBox, player loses 6 HP/mob/second
7. When player health reaches 0 → Game Over screen shows, game pauses
