# MindFlip Runner — README

A single-file, browser-based 2D endless runner with control-inverting mechanics.
No server needed. No install. Open the HTML file and play.

---

## How to Play

Open `MindFlipRunner.html` in any modern browser (Chrome, Firefox, Safari, Edge).

### Controls

| Action       | Desktop              | Mobile          |
|--------------|----------------------|-----------------|
| Move Left    | ← Arrow / A          | Tap LEFT button |
| Move Right   | → Arrow / D          | Tap RIGHT button|
| Jump         | Space / W / ↑ Arrow  | Tap JUMP button |

> **The Twist:** At random intervals your LEFT and RIGHT controls swap.
> The HUD shows NORMAL or FLIPPED — watch it!
> Jump is never inverted. Only left/right flips.

---

## Platform Types

| Color  | Type      | Behavior                                          |
|--------|-----------|---------------------------------------------------|
| Cyan   | Static    | Normal solid platform                             |
| Purple | Moving    | Slides left or right continuously                 |
| Orange | Crumble   | Shakes then falls ~0.9s after you land            |
| Green  | Conveyor  | Pushes you in the arrow direction                 |
| Yellow | Blink     | Disappears and reappears every ~0.8s              |
| Red outline | Phase Gate | Triggers an immediate control flip on touch |

---

## Game Systems

- **Flip Warning:** 0.5s before every flip, text flashes on screen and the color palette shifts warm (flipped) or cool (normal). Use this window to prepare.
- **Snap-Back Trap:** When controls return to normal, your brain will misfire again — this is intentional.
- **Speed Scaling:** Speed increases every meter. Flips happen more frequently as distance grows.
- **Procedural Chunks:** Levels are built from hand-designed 5-second chunks stitched randomly. Every run feels different but is always beatable.
- **Data Shards:** Yellow diamonds floating mid-air. Risky to collect, no gameplay effect — score flex only.
- **Best Score:** Saved to browser localStorage. Persists across sessions.

---

## Files

```
MindFlipRunner.html   — The entire game (HTML + CSS + JS, single file)
README.md             — This file
```

---

## Browser Compatibility

| Browser         | Status  |
|-----------------|---------|
| Chrome 90+      | ✅ Full  |
| Firefox 88+     | ✅ Full  |
| Safari 14+      | ✅ Full  |
| Edge 90+        | ✅ Full  |
| Mobile Chrome   | ✅ Full  |
| Mobile Safari   | ✅ Full  |

Requires: Canvas 2D API, requestAnimationFrame, localStorage.
No external dependencies. No internet connection required after first load
(Google Fonts load from CDN — game works without them, fonts fall back gracefully).

---

## Performance Notes

- Runs at 60fps on all modern devices.
- Off-screen platforms are culled from rendering every frame.
- Old platforms (far left of world) are removed from memory automatically.
- Delta-time capped at 50ms to prevent physics explosions on tab switch.
- No audio engine (keeping it lag-free and dependency-free).

---

## Known Limitations

- No audio (by design — keeps the file lightweight and universally compatible).
- Best score stored per browser (no cloud save).
- Versus mode and full progression system described in the GDD are not included in this prototype.

---

## Customization Quick Reference

Open the HTML file and find these constants near the top of the `<script>` tag:

```js
const GRAVITY      = 0.55;    // Higher = falls faster
const JUMP_FORCE   = -13.5;   // More negative = higher jump
const MOVE_SPEED   = 5.2;     // Player horizontal speed
const PLATFORM_H   = 18;      // Platform height in pixels
```

To change flip frequency, edit `scheduleNextFlip()`:
```js
function scheduleNextFlip() {
  const base = Math.max(4, 10 - G.distance / 200); // 4–10 seconds between flips
  G.nextFlipIn = base + Math.random() * 4;
}
```

---

Made with: HTML5 Canvas · Vanilla JS · Orbitron + Share Tech Mono (Google Fonts)
