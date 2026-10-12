# Stashman

A Smash-style 2D platform fighter for two players on one keyboard. Build damage, get launched, and be the last fighter standing.

Stashman is a single self-contained `index.html`: Canvas 2D, no build step, no libraries, no external assets.

## Play

Open `index.html` in a modern browser, or serve the folder:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

The game is also deployed to GitHub Pages on every push to `main` (see `.github/workflows/deploy.yml`).

## Controls

| Action        | Player 1 (EMBER) | Player 2 (TIDE) |
|---------------|------------------|-----------------|
| Move          | `A` / `D`        | `←` / `→`       |
| Jump / double jump | `W`         | `↑`             |
| Drop through one-way platform | `S` | `↓`        |
| Attack        | `F`              | `/`             |

Global keys:

| Key | Action                          |
|-----|---------------------------------|
| `R` | Rematch (on the winner screen)  |
| `M` | Toggle sound                    |

## Rules

- Two fighters, three stocks each.
- Damage (%) builds on every hit. Higher damage means harder knockback and longer hitstun.
- One double jump per airtime, restored on landing.
- Leaving the stage past a blast zone costs a stock. The fighter respawns from above with brief invulnerability (flicker).
- Last fighter with stocks wins.

## Design notes

- **Fixed 60 Hz simulation** with an accumulator. Rendering runs on `requestAnimationFrame` and interpolates between ticks.
- **Deterministic sim.** Physics and combat never call `Math.random()`. Randomness is limited to particles, screen shake, and audio noise, which never feed back into the simulation. This is the groundwork for rollback netcode.
- **Camera** follows the midpoint of living fighters, zooms out as they separate and in as they close, and clamps to the stage bounds.

## Roadmap

- [x] **Phase 1: Local 2-player Smash-like.** Core movement, combat, stocks, camera, HUD, juice.
- [ ] **Phase 2: Sprite system.** Replace procedural fighters with a sprite pipeline and animation frames while keeping the sim unchanged.
- [ ] **Phase 3: Menus.** Title screen, character select, stage select, pause menu, and options (controls, sound).
- [ ] **Phase 4: Online multiplayer.** Rollback netcode built on the deterministic simulation.

## Repository layout

```
index.html                      the complete game
README.md                       this file
.github/workflows/deploy.yml    GitHub Pages deployment
```
