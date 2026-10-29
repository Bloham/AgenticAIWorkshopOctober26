# Art drop-off

Everything visual for the workshop lands here. Two folders:

- **`incoming/`** — your finished files, exactly as you made them
- **`incoming/sound/`** — recorded sounds, music loops (`.wav`, `.ogg`)

You do not need git for this. Use the browser.

---

## Upload in four steps

1. Open **https://github.com/Bloham/AgenticAIWorkshopOctober26/tree/main/art/incoming**
2. **Add file → Upload files**
3. Drag your file in
4. **Commit changes**

New files never cause conflicts, so uploading straight to `main` is safe.

Then **say the filename out loud** — in the workshop chat or on the whiteboard. A coder cannot use a file they don't know exists.

---

## Naming

```
player-car-anna.png
enemy-robot-tomas.png
item-key-sofia.png
background-forest-anna.png
sound/hit-tomas.wav
sound/music-loop-sofia.ogg
```

`thing-what-it-is-yourname.ext` — lowercase, dashes, no spaces, your name last.
Your name stays in the filename even after the coder moves the file into the
project, so everyone can see who made what.

---

## Specs that save you a re-upload

| | |
|---|---|
| Format | **PNG with transparency** (sound: `.wav` or `.ogg`) |
| Background | fully transparent — use [remove.bg](https://www.remove.bg) if you photographed paper |
| Size | characters and props **256–512 px** on the long side; backgrounds 1024 px+ |
| Direction | draw characters **facing right**; the game flips them when needed |
| Shadow | no baked-in shadow unless you want it visible in game |
| Animations | one folder per thing, numbered frames: `incoming/player-car/frame-01.png`, `frame-02.png` |

**The white box problem.** A PNG with a white background looks like a white
rectangle in the game. It is the single most common mistake in this workshop.
Check for transparency before you upload — open the file, the background should
be a checkerboard pattern, not white.

---

## Paper to game in five minutes

1. Rough sketch on scrap paper — 30 seconds, no detail
2. Redraw bigger on A4, pencil
3. Trace the outlines with a thick marker
4. Colour it
5. Photograph it flat, phone directly above, good light
6. Remove the background in the browser
7. Upload
8. Tell the coders

Bold outlines and simple shapes survive the photo step best. Detail you can't
see in the photograph is detail that doesn't exist in the game.

---

## What happens after you upload

A coder points the game at your sprite, or asks the AI agent to do it. Godot
imports the PNG automatically within seconds. If your sprite does not appear,
the editor usually just needs a reimport — say so, don't redraw.

If your art gets moved into a project folder, the filename keeps your name. If
you want a different credit, or no credit, tell the facilitator.
