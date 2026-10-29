# Agentic AI Workshop — October 2026

A hands-on game development workshop at **Novia, Jakobstad**. Everyone gets their own computer, their own AI coding agent, and a working Godot game to change. At the end we film what you built.

**You are not starting from zero.** The game in this repository already runs: a player who moves and shoots, enemies that chase, a survival loop, health, a game-over screen. Your job today is to make it *yours* — and AI does the typing.

---

## What you need

- **Godot 4.6** — [godotengine.org/download](https://godotengine.org/download). Any 4.6.x build works. Older 4.x versions will complain about this project.
- **Git** or [GitHub Desktop](https://desktop.github.com) — or no git at all, if you only upload art through the browser (see below).
- An AI coding agent — your workshop account. It opens this folder and edits the game when you describe what you want.

---

## Quick start

```bash
git clone https://github.com/Bloham/AgenticAIWorkshopOctober26.git
cd AgenticAIWorkshopOctober26
```

Open the folder in Godot (Project Manager → Import → pick `project.godot`) and press **F5**. You should be running around shooting slimes within a minute.

First time in a fresh copy: the editor imports assets, which takes a few seconds. Ignore the `.godot/` folder — Godot rebuilds it locally and it is not in git.

---

## The rule that matters

**What is in the build is what counts.** A drawing on your desk, a script in the editor, a branch nobody merged — none of it exists. Get it into `main` and get it running in the game. Small and playable beats big and half-finished.

---

## How we work — four lanes

| Lane | What you do | Where it goes |
|---|---|---|
| **Art** | Draw, photograph, clean up, upload | `art/incoming/` |
| **Code** | Describe the change to your AI agent, test it in Godot | branch → pull request |
| **Sound & Music** | Record with a phone, or compose in the browser (BeepBox) | `art/incoming/sound/` |
| **Story & UI** | Game title, intro text, dialogue, HUD labels | `docs/story.md` |

Pick one. Stay in it. Tell the room what you are doing so two people don't build the same thing.

---

## Art pipeline

You do **not** need to know git to contribute art. Use the browser.

1. **Sketch small** — rough thumbnail on scrap paper, 30 seconds, just to fix the idea.
2. **Redraw on A4** — bigger and cleaner, in pencil.
3. **Trace with a thick marker** — bold outlines survive the photograph.
4. **Colour it** — markers or coloured pencils.
5. **Photograph it flat** — phone, directly above, good light, no shadow.
6. **Remove the background** — [remove.bg](https://www.remove.bg) in the browser, or Photopea/GIMP. The PNG must have **transparency**, otherwise your sprite shows as a white box in the game.
7. **Upload it** — open [art/incoming](https://github.com/Bloham/AgenticAIWorkshopOctober26/tree/main/art/incoming) → **Add file → Upload files** → drag the PNG in → **Commit changes**.
8. **Say the filename out loud** — in the workshop chat or on the whiteboard. Coders can't use what they can't find.

### File naming and specs

```
art/incoming/player-car-anna.png
art/incoming/enemy-robot-tomas.png
art/incoming/sound/hit-anna.wav
```

- lowercase, dashes, no spaces, end with your name — so we can see who made what.
- characters and props: **256–512 px** on the long side. Backgrounds: 1024 px or more.
- draw your character **facing right**; the code flips it when needed.
- animations: one folder per thing, numbered frames — `art/incoming/player-car/frame-01.png`, `frame-02.png`, …
- transparent background, no baked-in shadow unless you want it in game.

Want to go straight from paper to game in five minutes? Draw it, photograph it, upload it, and tell the coder department. That loop is the whole workshop.

---

## Code lane — git in six commands

```bash
git pull                                   # 1. get everyone's latest work first
git checkout -b code/your-name             # 2. your own branch
# ... change files, or let your agent change them ...
git add -A && git commit -m "add car player"   # 3. commit
git push -u origin code/your-name          # 4. push
```

Then open a **Pull Request** on GitHub and ask the facilitator to merge it. One PR per person, one idea per PR.

Conflict? You and someone else edited the same file or scene. Do not force-push. Ask the facilitator — merging a broken scene costs ten minutes, and we only have two hours.

**Practicals**

- Always `git pull` before you start, and before you open a PR.
- Never commit `.godot/`, your personal `export_presets.cfg`, or any password.
- Godot merges `.tscn` files badly. If two people must edit the same scene, edit it in turn, not in parallel.
- Everything is public. Don't upload anything you don't own or can't share.

---

## What is in here

```
project.godot           the Godot project — open this
survivors_game.tscn     main scene: player, spawner, game over
player.gd / mob.gd      player controller, enemy chase AI
gun.gd / bullet_2d.gd   auto-aim weapon, projectile
game.gd                 spawner + game-over logic
characters/ pistol/ trees/ smoke_explosion/   sprites and effects
art/incoming/           your uploads land here
docs/story.md           title, intro text, dialogue, HUD wording
AGENTS.md               tells your AI agent how to read this project
PROJECT_OVERVIEW.md     the full scene tree, scripts, collision layers
```

If you use an AI agent, `AGENTS.md` and `PROJECT_OVERVIEW.md` are why it can help you fast — the agent reads them before touching anything. Keep `PROJECT_OVERVIEW.md` honest if you change the architecture.

---

## Credits and licence

- Base project built from GDQuest's free course [Your First 2D Game in Godot 4](https://www.gdquest.com/library/first_2d_game_godot4_vampire_survivor/). Graphics by GDQuest, **CC BY 4.0**. See [ATTRIBUTION.md](ATTRIBUTION.md).
- Workshop code and material: **MIT** — see [LICENSE](LICENSE).
- Anything you draw, compose or write today stays **yours**. By uploading it here you agree it can stay in this public repository under CC BY 4.0, credited to you.

---

## Credits to people, not just licences

Organised by Benjamin Vehling (Tysk Games / Novia) with Bothnia Game Devs. Run at Novia Jakobstad, October 2026.

*The Door Problem* by Liz England — [gamedeveloper.com](https://www.gamedeveloper.com/design/-quot-the-door-problem-quot-of-game-design) — is the reason this workshop has departments at all. Read it after today; it explains why every part of a game needs every kind of person.
