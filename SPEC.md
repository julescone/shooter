# Space Shooter — Game Spec

## Overview

A retro 2D vertical-scrolling space shooter built with HTML5 Canvas (single `index.html`, no dependencies). The player pilots a ship through **3 stages**, each ending with a boss fight. Every milestone is fully playable on its own.

---

## Core Requirements

| # | Requirement |
|---|---|
| R1 | Player moves in all 4 directions with WASD or Arrow keys |
| R2 | Player fires with Space or Z (hold to auto-fire) |
| R3 | Player has 3 lives; losing all lives triggers Game Over |
| R4 | 2-second invincibility window after taking a hit (ship flickers) |
| R5 | Enemies spawn from the top and scroll down |
| R6 | Enemies fire aimed projectiles at the player |
| R7 | 3 enemy tiers — small (1 HP), medium (3 HP), big/boss (20 HP) |
| R8 | Score increases per enemy killed (small 100 pts, medium 250, boss 1000) |
| R9 | Power-ups drop from destroyed enemies (~20% chance) |
| R10 | Each stage ends when its boss is destroyed |
| R11 | Stage clear screen shown between stages |
| R12 | Game Over screen shows final score with restart option |

### Power-up types

| Sprite | Effect | Duration |
|--------|--------|----------|
| power-up1 | Speed boost (1.6×) | 8 s |
| power-up2 | Twin shot (2 guns) | 10 s |
| power-up3 | Spread shot (3-way) | 10 s |
| power-up4 | Extra life (instant) | — |

---

## Pixel Art Assets

All paths are relative to the project root (`shooter/`).

### Player Ship
| Asset | Path |
|-------|------|
| Ship frames 1–10 (banking animation) | `Legacy Collection/Legacy Collection/Assets/Packs/SpaceShipShooter/Sprites/Ship/ship1.png` … `ship10.png` |

### Enemies
| Asset | Path |
|-------|------|
| Small enemy frame 1–2 | `Legacy Collection/Legacy Collection/Assets/Packs/SpaceShipShooter/Sprites/EnemySmall/enemy-small1.png` … `enemy-small2.png` |
| Medium enemy frame 1–2 | `Legacy Collection/Legacy Collection/Assets/Packs/SpaceShipShooter/Sprites/Enemy Medium/enemy-medium1.png` … `enemy-medium2.png` |
| Big enemy / boss frame 1–2 | `Legacy Collection/Legacy Collection/Assets/Packs/SpaceShipShooter/Sprites/EnemyBig/enemy-big1.png` … `enemy-big2.png` |

### Effects
| Asset | Path |
|-------|------|
| Explosion frames 1–5 | `Legacy Collection/Legacy Collection/Assets/Packs/SpaceShipShooter/Sprites/Explosion/explosion1.png` … `explosion5.png` |
| Power-up sprites 1–4 | `Legacy Collection/Legacy Collection/Assets/Packs/SpaceShipShooter/Sprites/PowerUps/power-up1.png` … `power-up4.png` |

### Backgrounds
| Asset | Role | Path |
|-------|------|------|
| blue-back.png | Deep-space layer (slowest) | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/blue-back.png` |
| blue-stars.png | Star field layer (medium) | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/blue-stars.png` |
| blue-with-stars.png | Combined starfield (stage 3) | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/blue-with-stars.png` |
| prop-planet-small.png | Drifting prop (stages 1–2) | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/prop-planet-small.png` |
| prop-planet-big.png | Drifting prop (stage 3) | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/prop-planet-big.png` |
| asteroid-1.png | Hazard prop | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/asteroid-1.png` |
| asteroid-2.png | Hazard prop | `Legacy Collection/Legacy Collection/Assets/Environments/space_background_pack/Blue Version/layered/asteroid-2.png` |

---

## Milestones

### Milestone 1 — Playable Core

**Goal:** A working game loop you can actually play, with the most essential mechanics only.

**Delivers:**
- HTML Canvas at 480×720, 60 fps game loop
- Parallax scrolling background (`blue-back` + `blue-stars` layers)
- Player ship renders and moves (WASD / arrows), clamped to screen
- Single-shot auto-fire (Space / Z)
- Static ship sprite (no banking yet)
- Stage 1 only: small enemies spawn in waves, sinewave movement toward bottom
- Bullet ↔ enemy collision (enemies die in one hit)
- Bullet ↔ player collision (instant death, no lives yet — restart on death)
- Score counter (top-left HUD)
- Game Over screen with score + "Press Enter to restart"
- Stage 1 ends after 5 waves of small enemies

**Not yet included:** lives, explosions, enemy fire, power-ups, boss, banking animation.

---

### Milestone 2 — Full Combat Loop

**Goal:** A complete single-stage experience with everything a shmup needs to feel good.

**Adds on top of M1:**
- 3 lives + invincibility flicker (R3, R4)
- Lives displayed as ship icons (top-right HUD)
- 2-frame enemy animation
- Ship banking animation (frames 1–10 based on horizontal movement)
- Explosion effect on enemy and player death (5-frame animation)
- Enemies fire aimed projectiles at the player
- HP bars on medium enemies (3 HP) and boss (20 HP)
- Stage 1 boss: big enemy appears after wave 5, centred at top, higher HP, faster fire rate
- Boss death → "Stage Clear" screen → restart from Stage 1
- Power-ups drop on enemy death; all 4 types functional

---

### Milestone 3 — All 3 Stages

**Goal:** The full game — three distinct stages with increasing difficulty, each with a boss.

**Adds on top of M2:**

| Stage | Enemy mix | Boss HP | BG extras | Scroll speed |
|-------|-----------|---------|-----------|--------------|
| 1 | Small only | 20 | `prop-planet-small` drifting | 1× |
| 2 | Small + Medium | 30 | `prop-planet-big` drifting | 1.3× |
| 3 | Small + Medium + strafing Big | 40 | `blue-with-stars` layer + asteroid props | 1.6× |

**Also adds:**
- Title / start screen (ship animated in background)
- Stage intro card ("STAGE 1", "STAGE 2", "STAGE 3") with 2 s delay before enemies appear
- Persistent high score stored in `localStorage`
- After Stage 3 boss dies → "YOU WIN" screen with score and high score
- Enemy spawn interval tightens each wave (max pressure cap per stage)
