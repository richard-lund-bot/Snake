# LCD Arcade

A tiny Nokia/LCD-style mini-game collection in a single `index.html` — no build
step, no dependencies. Swipe, tap the on-screen D-pad, or use the keyboard. Add
it to your home screen to play full-screen.

## Games
- **Snake** — the classic. Eat the dots, don't hit the walls or yourself.
- **Don't Blink** — foes creep toward you only while you're *not* watching them.
  Aim your gaze (a 90° wedge) to freeze a whole side; survive as long as you can.

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
