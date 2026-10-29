# Agentic AI Workshop — October 2026

A hands-on game development workshop at **Novia, Jakobstad**. Everyone gets their own computer, their own AI coding agent, and a working Godot game to change. At the end we film what you built.

**You own one feature, from beginning to end** — the art, the sound, the code, and getting it into the game. Not a department, not one slice of someone else's idea. Your enemy or your item, start to finish.

---

## What you need

- **Godot 4.6** — [godotengine.org/download](https://godotengine.org/download). Any 4.6.x build works.
- **Git** or [GitHub Desktop](https://desktop.github.com)
- An AI coding agent — your workshop account. It opens this folder and edits the game when you describe what you want.
- **Krita** (installed) or a browser for [Photopea](https://www.photopea.com) and [bfxr](https://www.bfxr.net)

---

## Quick start

```bash
git clone https://github.com/Bloham/AgenticAIWorkshopOctober26.git
cd AgenticAIWorkshopOctober26
```

Open the folder in Godot (Project Manager → Import → pick `project.godot`) and press **F5**. You should be running around shooting slimes within a minute.

---

## Your job today

1. **Pick a feature** — an enemy or an item. One. Write your name on the board next to it so nobody doubles up.
2. **Copy the template** into a folder with your name.
3. **Draw it** digitally — no paper. Krita or Photopea, transparent PNG.
4. **Give it a sound** — record something, or generate one in bfxr.
5. **Build it** with your agent, test it with **F6**.
6. **Register it** — one line in `features/enemies.txt` or `features/items.txt`.
7. **Press F5.** Your feature is in the game. Ship it with a Pull Request.

Full instructions, with sizes and naming: **[features/README.md](features/README.md)**.

---

## The rule that matters

**What is in the build is what counts.** A drawing in your folder, a script in the editor, a branch nobody merged — none of it exists. Registered and running in the game, with the whole group playing, is the finish line.

A simple enemy that works beats an ambitious one that doesn't.

---

## How the project fits together

```
project.godot            the Godot project — open this
survivors_game.tscn      main scene: player, spawner, game over
player.gd / mob.gd       player controller, enemy chase AI
gun.gd / bullet_2d.gd    auto-aim weapon, projectile
game.gd                  spawner + game-over logic

features/
  enemies.txt            ← register your enemy here
  items.txt              ← register your item here
  library.gd             the autoload that loads registered features
  _template/enemy/       copy this for an enemy
  _template/item/        copy this for an item
  yourname-thing/        your feature lives here, and only yours

docs/story.md            title, intro text, HUD wording — if you want to write instead
AGENTS.md                tells your AI agent how to read this project
PROJECT_OVERVIEW.md      the full scene tree, scripts, collision layers
```

The game asks `FeatureLibrary` for a random enemy or item whenever it spawns
something. `FeatureLibrary` reads the two manifest files. That is the whole
integration — which is why nobody has to edit a shared scene to get their work
into the game.

---

## Working with others

- **Always `git pull` before you start**, and again before you open a Pull Request.
- **Stay in your folder.** The shared files (`game.gd`, `player.gd`, `features/library.gd`) are the wiring everyone depends on.
- **Your own scene is never merged by anyone else**, so Godot's scene-merge problem only bites if you edit someone else's.
- **Conflict on `enemies.txt`?** Keep both lines. That file is almost impossible to break.
- **Never commit `.godot/`, `export_presets.cfg`, or a password.** Everything here is public.

---

## Credits and licence

- Base project built from GDQuest's free course [Your First 2D Game in Godot 4](https://www.gdquest.com/library/first_2d_game_godot4_vampire_survivor/). Graphics by GDQuest, **CC BY 4.0**. See [ATTRIBUTION.md](ATTRIBUTION.md).
- Workshop code and material: **MIT** — see [LICENSE](LICENSE).
- Anything you draw, compose or write today stays **yours**. By uploading it here you agree it can stay in this public repository under CC BY 4.0, credited to you — your name is in your folder and in your filenames.

---

## Credits to people, not just licences

Organised by Benjamin Vehling (Tysk Games / Novia) with Bothnia Game Devs. Run at Novia Jakobstad, October 2026.

*The Door Problem* by Liz England — [gamedeveloper.com](https://www.gamedeveloper.com/design/-quot-the-door-problem-quot-of-game-design) — explains why a game needs artists, programmers, and everyone in between to agree on what a door even is. Today, for one feature, you are all of them at once.
