# Hot Dog Dash

An HTML5 first-person parkour game, deployed on Cloudflare Pages and embedded (iframe) into another website.

A seaside carnival boardwalk where time only moves when you do. The hot dog vendors have had enough:
they wind up (a mustard telegraph line), hurl hot dogs, and the hot dogs hang in the air while you stand still.
Run, jump, slide, mantle and wall-run down the pier; dodge the dogs, shove vendors at arm's reach,
or let them pelt each other. Every hot dog carries a pulsing ring (red once it's in reach). When one gets close,
time snaps into slow-mo and a click **smacks** it back toward whatever you're looking at — vendors, or the boss.
A procedural xylophone track (16-step sequencer, kick/snare/hat, bass) plays throughout; it muffles as time slows
and speeds up in the boss zone. Vendors yell at you in autotune (word-by-word speech synthesis snapped to a pentatonic
scale with a synth harmony underneath); only vendors within ~24 m are audible.

**The Big Wiener** — a ~180 m hot dog standing in the sea at the end of the pier — is visible from the moment you spawn
and grows as you run (it's exempt from fog and hazed by distance instead). The pier bridges into an arena at its feet
(560 m); there it winds up and lobs giant hot dogs down at you. In the arena you get a ketchup gun (left click / Q) and a mustard gun (right click / E). The boss
alternates which condiment it "wants" (shown under its HP bar); matching hits do 3 damage, the other does 1.
Condiments also knock hot dogs — even the giant ones — out of the air. Beat it for the win screen.

- `public/index.html` — the entire game (no build step; Three.js is loaded from a CDN)
- `wrangler.jsonc` — Cloudflare Pages config (`pages_build_output_dir: ./public`)

## Controls

| Input | Action |
| --- | --- |
| WASD / arrows | move |
| Mouse | look (pointer lock) |
| Space | jump, wall-jump |
| Shift | slide |
| Click | smack a close hot dog · shove a vendor · ketchup gun in the arena |
| Right click / E | mustard gun (arena only) |
| Air + wall + forward | wall-run |
| M | mute |

Touch devices get a virtual joystick, drag-to-look, and JUMP / SHOVE buttons (plus MUSTARD in the arena).

## Versioning

The version shows in the bottom-right corner of the game. To release a new version, bump
`VERSION` (and the matching `<meta name="version">` and `#ver` text) at the top of `public/index.html`,
commit, and tag it: `git tag v1.1.0 && git push --tags`.

## Run locally

    python3 -m http.server 8000 -d public

## Deploy

    npx wrangler pages deploy

## Embed

    <iframe src="https://<your-pages-domain>/" width="960" height="600" style="border:0" allow="pointer-lock; fullscreen"></iframe>

The game fills whatever size the iframe is. `allow="pointer-lock"` is required for mouse look inside a cross-origin iframe
(without it the game falls back to click-and-drag look).
