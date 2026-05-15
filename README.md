# Droidex Tracker

A single-page tracker for **Star Wars Droid Tycoon** in Fortnite — built so I can keep tabs on which droids I still need to build and upgrade while I'm standing in front of the Sandcrawler conveyor belt waiting for blueprints to scroll past.

Hosted as a GitHub Pages static site (see _Running it_ below), so I can just pull it up on my phone in a second tab while playing.

## Why this exists

The Droidex has 200+ droids across four upgrade tiers — **Default → Gold → Diamond → Rainbow** — and the conveyor belt at the Jawa Sandcrawler only cycles through a handful at a time. The in-game Droidex UI is fine for browsing, but it's slow to use as a "what am I still missing right now" checklist when you only have a couple of seconds before a blueprint disappears off the belt.

This page is purpose-built for that one job:

- Open it, glance at the row, decide if I want it, look back at the conveyor.
- Filtered by default to show only the droids/tiers I haven't completed yet.
- Tier columns I've already finished go dark and recede; the ones I still need stay vivid.
- Tap a button to mark something built — state saves in `localStorage`, so it's there next time I open it.

## Features

- **Grid view**: rows of droids × four tier columns (Default / Gold / Diamond / Rainbow). Each cell shows the credits-per-second income that tier generates and the Upgrade Chips required to reach it.
- **Compact mode**: collapses every droid to a single line with four tap-to-toggle tier pills — useful on mobile and when you just want a quick "did I do this one?" scan.
- **Filters**: search by name, filter by rarity (Common → Mythic), and an _Only droids I still need_ toggle that hides anything fully complete.
- **Sorting**: alphabetical (A↔Z) or by rarity (low↔high).
- **Done = dim**: completed tiers fade to near-black; the things you still need to grab pop in gold / hologram-cyan / rainbow.
- **Rarity stripes**: each row has a colored left edge so Common / Rare / Epic / Legendary / Mythic are recognisable at a glance.
- **No build step, no dependencies**: a single `index.html`. Open it locally with a double-click, or host it as a static site.
- **Persists locally**: completion state lives in your browser's `localStorage`. Clearing site data resets it. There's also a manual _Reset_ button that restores the initial "still to build" list.

## Running it

### Locally

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

That's it — there's nothing to install.

### GitHub Pages

After pushing to GitHub:

1. Go to the repo on github.com → **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to _Deploy from a branch_.
3. Pick branch **`main`** and folder **`/ (root)`**. Save.
4. After a minute or so the site will be available at `https://<your-username>.github.io/droidex/`.

Because it's a single static HTML file, no Jekyll/GitHub Actions setup is needed.

## Initial state

On first run **nothing is marked as built** — every droid × tier cell starts empty so you can tick off entries as you collect them at the Sandcrawler. The **Reset** button (top right) clears everything back to that empty state.

## Storage & privacy

This site stores your completion ticks and your compact-mode preference in your browser's `localStorage`. That's not a cookie — it's a separate browser API that:

- never leaves your device,
- is never sent in HTTP requests,
- isn't shared with any third party,
- is strictly functional (it only remembers what _you_ ticked).

Because of that it qualifies as "strictly necessary for the service requested by the user" under the EU ePrivacy Directive / GDPR, so no consent banner is required.

The page does load the Orbitron / Rajdhani fonts from Google Fonts via CDN; if you want the page to be 100% first-party with no external requests, swap the `<link>` tags for self-hosted font files.

## Data sources

Droid names, rarities, types, and credits/sec per tier come from [Insider Gaming's Droidex](https://insider-gaming.com/fortnite-star-wars-droid-tycoon-droidex-all-droids/). Upgrade Chip costs come from their [upgrade-cost breakdown](https://insider-gaming.com/fortnite-star-wars-droid-tycoon-upgrade-droids/) and the [GAMES.GG upgrade guide](https://games.gg/fortnite/guides/fortnite-how-to-upgrade-droids-and-all-costs/). Mythic-tier costs (BB-8, Mister Bones) are TBC by the game.

## Stack

- One file: `index.html`.
- Vanilla HTML, CSS, JavaScript — no framework, no bundler, no npm.
- Google Fonts for Orbitron / Rajdhani (loaded via CDN).
- `localStorage` for state persistence.
