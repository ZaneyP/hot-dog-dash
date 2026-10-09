# Hot Dog Dash

An HTML5 first-person parkour game, deployed on Cloudflare Pages and embedded (iframe) into another website.

A seaside carnival boardwalk where time only moves when you do. The hot dog vendors have had enough:
they wind up (a mustard telegraph line), hurl hot dogs, and the hot dogs hang in the air while you stand still.
Run, jump, slide, mantle and wall-run down the pier; dodge the dogs, shove vendors at arm's reach,
or let them pelt each other. Every hot dog carries a pulsing ring (red once it's in reach). When one gets close,
time snaps into slow-mo and a click **smacks** it back toward whatever you're looking at — vendors, or the boss.
A procedural xylophone track (16-step sequencer, kick/snare/hat, bass) plays throughout; it muffles as time slows
and speeds up in the boss zone. Vendors yell at you in autotune (word-by-word speech synthesis snapped to a pentatonic
scale with a synth harmony underneath); one vendor sings at a time, each word lands on a beat of the music, and only
vendors within ~24 m are audible. Your arm stays off-screen and jabs in from the bottom-right on a punch.

**The Big Wiener** — a ~180 m hot dog standing in the sea at the end of the pier — is visible from the moment you spawn
and grows as you run (it's exempt from fog and hazed by distance instead). The pier bridges into an arena at its feet
(560 m); there it winds up and lobs giant hot dogs down at you. The fight is a duel of reflexes: when a giant dog gets
close, time snaps into slow-mo — smack it and it flies straight back into his chest. Six returned dogs finish him
(hitstop, camera shake and a stagger on every hit; at three he goes ENRAGED and throws twice). On the last hit he
topples backward into the sea.

- `public/index.html` — the entire game (no build step; Three.js is loaded from a CDN)
- `wrangler.jsonc` — Cloudflare Pages config (`pages_build_output_dir: ./public`)

## Controls

| Input | Action |
| --- | --- |
| WASD / arrows | move |
| Mouse | look (pointer lock) |
| Space | jump, wall-jump |
| Shift | slide |
| Click / right click | smack a close hot dog · shove a vendor |
| Air + wall + forward | wall-run |
| M | mute |

Touch devices get a virtual joystick, drag-to-look, and JUMP / SHOVE buttons.

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
