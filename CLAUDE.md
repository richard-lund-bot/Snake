# LO-FI Arcade

A single self-contained `index.html` — a tiny LCD-handheld arcade (Snake, Don't
Blink, Mirror Twins, Polarity) with a lofi, score-driven seasonal theme. No build
step and no test suite: open `index.html` in a browser to run it. A real browser
is the source of truth — palette, atmosphere, particles, and audio can't be fully
judged from the code alone.

## Deploy / live testing (important — standing instruction from the owner)

The owner always tests on the **live GitHub Pages site**, which is served from the
"published build" branch — currently **`claude/magical-dirac-f2c9f1`** (identify it
as the branch whose commits read "Sync published build with main"; `main` is the
source of record but is NOT the published branch). Merging to `main` does **not**
update the live site by itself.

**Always make new work testable on the live site.** Once changes are on `main`,
sync the publish branch and push:

```sh
git checkout -B claude/magical-dirac-f2c9f1 origin/claude/magical-dirac-f2c9f1
git checkout origin/main -- index.html        # the site is just this one file
git commit -m "Sync published build with main: <summary>"
git push origin claude/magical-dirac-f2c9f1
git checkout <your working branch>            # return to the assigned dev branch
```

This is the one expected exception to "don't push to a branch other than the
assigned working branch": the owner has given standing approval to keep the
published branch in sync so the live site always reflects the latest work.
