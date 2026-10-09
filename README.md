# TEMPO

An HTML5 first-person parkour game, deployed on Cloudflare Pages and embedded (iframe) into another website.

Time only moves when you move. Special agents have been assigned to eliminate you: they take aim
(a red telegraph line), fire, and their bullets crawl through the air while you stand still. Run,
jump, slide, mantle and wall-run across endless rooftops; dodge the shots, punch agents at arm's
reach, or let them shoot each other. Score is distance travelled.

- `public/index.html` — the entire game (no build step; Three.js is loaded from a CDN)
- `wrangler.jsonc` — Cloudflare Pages config (`pages_build_output_dir: ./public`)

## Controls

| Input | Action |
| --- | --- |
| WASD / arrows | move |
| Mouse | look (pointer lock) |
| Space | jump, wall-jump |
| Shift | slide |
| Click | punch |
| Air + wall + forward | wall-run |
| M | mute |

Touch devices get a virtual joystick, drag-to-look, and JUMP / PUNCH buttons.

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
