# Agent Instructions

You are working in a **Godot 4.6** 2D top-down survival shooter written in
**GDScript**, used in a two-hour workshop where the people prompting you are
beginners.

## Read this first

- **`PROJECT_OVERVIEW.md`** — full scene hierarchy, scripts, collision layers,
  assets and game flow. Always consult it before changing anything; it is the
  map of how the pieces connect.

## Workshop ground rules

1. **Small, working changes.** The workshop is two hours long. Prefer a change
   that runs over an ambitious one that half-works. One feature per request.
2. **Never touch `.godot/`.** It is a local editor cache, not source.
3. **Keep the project runnable.** After editing a `.gd` or `.tscn`, the game must
   still open and play. If you cannot verify it, say so explicitly instead of
   claiming success.
4. **Do not rename scenes, nodes or files** unless the request says so — renaming
   breaks `res://` paths across the project. If a rename is genuinely needed,
   update every reference in the same change.
5. **Do not delete assets** you did not create. If something looks unused, ask.
6. **Explain in one or two sentences** what you changed and where, so a beginner
   can follow. No walls of text.

## Project conventions

- GDScript only. Godot 4 syntax (`@onready`, `%UniqueNodeName`, typed hints where
  they help readability).
- Scenes use unique-name node access (`%Player`, `%HurtBox`, `%ShootingPoint`).
- Collision layers are documented in `PROJECT_OVERVIEW.md` — respect them; a
  bullet must hit enemies and not the player.
- Signal-driven where the existing code is: `health_depleted`, `died`.
- Art is referenced with `res://` paths.

## Where new assets come from

Participants upload art into **`art/incoming/`** through the GitHub web UI,
named like `player-car-anna.png` (lowercase, dashes, creator name at the end).
When asked to use a new sprite:

1. Look for the file in `art/incoming/`.
2. Move or reference it from a sensible place in the project if the request
   needs that, but keep the original filename recognisable so the artist's
   contribution stays visible.
3. Godot imports new PNGs on its own. If a texture does not appear, the editor
   needs a reimport — say that instead of inventing a code fix.

Sound files arrive as `.wav` / `.ogg` in `art/incoming/sound/`.

Story text, titles and HUD wording live in `docs/story.md`.

## Good first tasks for this project

- Change the player's movement speed or the firing rate (tuning, tiny diff).
- Swap a sprite: player, enemy, pistol, bullet, tree.
- Change enemy spawn interval, enemy speed or enemy health.
- Add a pickup that heals the player (`game.gd` spawner + a small `Area2D`).
- Add a title label or restart button on the game-over screen.
- Change the background colour or add a night overlay.

## What to avoid

- Adding plugins, packages or external dependencies during the workshop.
- Rewriting the architecture "properly" — the workshop needs the existing shape.
- Multi-file refactors when a one-line change would do.
- Committing `export_presets.cfg`, `.godot/`, or any credential.
