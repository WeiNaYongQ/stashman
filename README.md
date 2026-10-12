# Neon Ring

Neon Ring is a self-contained local two-player platform fighter built with the Canvas 2D API. Two chunky neon competitors share one keyboard, build damage through active-frame attacks, and launch each other out of a wide multi-platform arena. The camera smoothly tracks the living fighters and zooms to keep the duel readable.

There is no build step, package manager, library, or external asset. The complete game lives in [`index.html`](./index.html).

## Run locally

Serve the repository root with any static file server, then open the local URL:

```bash
python3 -m http.server 8000
```

Visit <http://localhost:8000>. Opening `index.html` directly also works in modern browsers, but a static server matches the GitHub Pages environment most closely.

## Controls

| Action | Player 1 — Lumen | Player 2 — Riot |
| --- | --- | --- |
| Move | `A` / `D` | `←` / `→` |
| Jump / double jump | `W` | `↑` |
| Drop through a floating platform | `S` | `↓` |
| Attack | `F` | `/` |
| Rematch after the match | `R` | `R` |

Jump and attack are edge-triggered: press the key rather than holding it. Arrow-key browser scrolling is suppressed while playing. Switching tabs or leaving the window clears held input.

## Game rules

- Each fighter starts with 3 stocks.
- Attacks deal 9% damage during their active frames and can hit each opponent only once per swing.
- Knockback and hitstun scale with the target's accumulated damage, so high-percent launches are dramatically stronger.
- A single double jump is available per airtime and resets on landing.
- The main platform is solid; the elevated platforms are one-way and can be dropped through with Down.
- Falling beyond the blast zone costs a stock and respawns the fighter with temporary flickering invulnerability.
- The final fighter with a stock remaining wins. Press `R` to reset the match.

## Deployment

The repository includes a GitHub Actions workflow at [`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml). Enable GitHub Pages with **GitHub Actions** as the source; pushes to `main` publish the repository root automatically. The workflow can also be started manually with `workflow_dispatch`.

## Roadmap

### Phase 2 — Sprite system

- Replace the procedural fighter silhouettes with an authored sprite-sheet pipeline.
- Add directional attack frames, hurt poses, landing poses, and animation timing tools.
- Keep the deterministic gameplay hitboxes separate from presentation frames.

### Phase 3 — Menus and match flow

- Add a title screen, fighter select, stage select, pause menu, and rematch settings.
- Add configurable key bindings, accessibility options, audio sliders, and a training mode.
- Expand the HUD with a move list and post-match results screen.

### Phase 4 — Online multiplayer

- Reuse the fixed 60 Hz deterministic simulation for input recording and rollback.
- Add a small authoritative session service, connection flow, latency display, and rollback diagnostics.
- Add spectator/replay support once synchronized inputs are reliable.
