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
close, time snaps into slow-mo — smack it and it flies straight back into his chest. Each returned dog takes a notch off his health bar
(hitstop, camera shake and a stagger on every hit; at half health he goes ENRAGED and throws twice). On the last hit he
topples backward into the sea.

## Levels

Five piers, each longer and meaner, with its own sky and its own giant at the end:

| # | Pier | Length | Boss | HP |
| --- | --- | --- | --- | --- |
| 1 | The Boardwalk | 560 m | The Big Wiener | 6 |
| 2 | Sunset Pier | 700 m | The Bratwurst Baron | 7 |
| 3 | Night Market | 820 m | The Kielbasa King | 8 |
| 4 | Storm Pier | 940 m | The Chili Dog Champion | 9 |
| 5 | The End of the Pier | 1100 m | The Wurst of All (enraged from the start) | 11 |

Each pier has its own vendors from around the boardwalk: hot dog vendors (pier 1), ice cream vendors whose cones
split into three scoops at the top of the arc (pier 2), cotton candy carnies lobbing huge slow floating clouds
(pier 3), ring-toss carnies throwing rings that home in on you (pier 4), and everything at once on pier 5. From
pier 2 on, seagulls perch above the pier and dive-bomb you when you get close. All of it is smackable.
Vendors start harder on later piers and the music tempo climbs. Clearing a pier unlocks the next (saved in
`localStorage`); press 1–5 on any menu to jump to an unlocked level. Beating all five brings up the VICTORY screen: fireworks, confetti, a
xylophone fanfare, your medals and campaign totals, with the camera slowly panning the arena.

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
