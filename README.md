# LO-FI Arcade

A tiny Nokia/LCD-style mini-game collection in a single `index.html` — no build
step, no dependencies. Steer with the on-screen D-pad or the keyboard. Add it to
your home screen to play full-screen.

## Games
- **Snake** — the classic. Eat the dots, don't hit the walls or yourself.
- **Don't Blink** — creatures freeze while you watch them and creep inward when
  you look away. *Hold* your gaze on a side (a 90° wedge) and those foes crumble
  to dust; sweep your gaze to pick off the nearest threats and outlast a slowly
  rising swarm. Score is foes banished. Rounds run ~1–3 min; experts go far longer.
- **Mirror Twins** — one D-pad drives two dots at once: the right twin mirrors
  the left (left/right are opposite, up/down shared). Run each twin over its
  pellet before that pellet's fuse burns out. Three lives; fuses shrink as you
  score, so the coupled controls get harder to satisfy.
- **Polarity** — walls fall with a gap marked **+** (solid) or **−** (hollow).
  Slide to the gap (Left/Right) and match your charge to it (Up = +, Down = −).
  Three lives; gaps wander wider and fall faster as you score.

Each game keeps its own top-10 high-score table (with 3-initial entry), stored
locally under a `hs:<game>` key.

## Adding a game
Games are plain objects in a registry inside `index.html`:

```js
register({
  id: 'mygame', title: 'MY GAME', grid: 16,
  reset(api) { /* set up state */ },
  tick(api, ts) { /* one logic step; api.addScore(n), api.gameOver(), api.win() */ },
  draw(api, ts) { /* api.block/head/dot/ring/beam(x,y) on the grid */ },
  onDir(dx, dy, api) { /* D-pad / swipe / arrows */ },
  stepMs(api) { return 130; }            // tick interval (may scale with score)
});
```

The shared "console" core handles the LCD shell, status bar, input, pause, the
home menu, and the high-score flow.
