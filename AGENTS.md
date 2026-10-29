# Agent Instructions

You are working in a **Godot 4.7** 2D top-down survival shooter written in
**GDScript**, used in a two-hour workshop where the people prompting you are
beginners.

## Read this first

- **`PROJECT_OVERVIEW.md`** — full scene hierarchy, scripts, collision layers,
  assets and game flow. Always consult it before changing anything; it is the
  map of how the pieces connect.
- **`features/README.md`** — the workflow each participant is following.

## The shape of the work

Each participant **owns exactly one feature** — one enemy or one item — and
builds it end to end: art, sound, code. Their work lives in **one folder**:

```
res://features/<studentname>-<featurename>/
```

They copy it from `features/_template/enemy/` or `features/_template/item/`.
Everything they need to change is inside their own folder.

**Stay inside the student's feature folder.** The rest of the project is shared
wiring that nineteen other people depend on.

## Ground rules

1. **Small, working changes.** Two hours, beginners. A change that runs beats an
   ambitious one that half-works. One request at a time.
2. **Never edit the shared wiring** unless the student explicitly asks and you
   explain why: `game.gd`, `player.gd`, `gun.gd`, `bullet_2d.gd`,
   `features/library.gd`, `.tscn` files outside their folder.
3. **Registering a feature is one line** in `features/enemies.txt` or
   `features/items.txt`. Tell the student to add it themselves — it is their
   finish line, and it is how they learn where the boundary is.
4. **Never touch `.godot/`.** It is a local editor cache, not source.
5. **Keep the project runnable.** After editing, the scene must still open and
   play. If you cannot verify it, say so instead of claiming success.
6. **Do not rename scenes, nodes or files** unless the request says so —
   renaming breaks `res://` paths. If it is genuinely needed, update every
   reference in the same change.
7. **Explain in one or two sentences** what you changed and where, so a beginner
   can follow. No walls of text.

## What a feature must keep true

The game depends on these; a feature that breaks them will not work when it
spawns in the real game, even if it looks fine in isolation.

**Enemy** (`CharacterBody2D`):
- `collision_layer = 2` — this is how bullets hit it and how touching it hurts the player
- has a `take_damage()` function — that is what bullets call
- chases the player (`get_tree().get_first_node_in_group("player")`)

**Item** (`Area2D`):
- `collision_layer = 0`, `collision_mask = 1` — it notices the player walking in
- on `body_entered`, checks `body.is_in_group("player")`, does something, then `queue_free()`
- may call `body.heal(amount)` on the player

Assets live in the feature folder: `art/` for PNGs (and the `.kra` working file),
`sound/` for `.wav`/`.ogg`. Godot imports new PNGs on its own; if a texture does
not appear, the editor needs a reimport — say that instead of inventing a code fix.

## Good requests you will get

- "Make it faster / slower" — tune the exported `speed` value.
- "Use my drawing" — assign the PNG to the Sprite2D texture.
- "It should shoot back" — add a projectile scene inside their folder.
- "Make it drop something when it dies" — spawn a small scene from the feature folder.
- "Make it bigger / smaller / glow / flash" — modulate, scale, tween.
- "Add the sound" — assign `death_sound` / `pickup_sound`, or add an `AudioStreamPlayer2D`.
- "Make my item give speed instead of health" — change what happens on pick-up.

## What to avoid

- Adding plugins, packages or external dependencies during the workshop.
- Rewriting the architecture "properly" — the workshop needs the existing shape.
- Editing another student's feature folder.
- Multi-file refactors when a one-line change would do.
- Committing `export_presets.cfg`, `.godot/`, or any credential.
