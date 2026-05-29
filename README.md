# Color Dash Galaxy

A top-down arcade space shooter that fuses **bullet hell** with a **color-matching** mechanic. Cycle your ship between red, blue and yellow: you can only be hit by enemies of a *different* colour, and your bullets only destroy enemies of the *same* colour. Survive the swarm, master the colour switch, and take down the three-part boss.

Built in Unity 2019.4 (C#, Universal Render Pipeline) as my final project for the BSc Computer Science programme (CM3070) at the University of London.

> **▶ Download & play:** [eleceb.itch.io/color-dash-galaxy](https://eleceb.itch.io/color-dash-galaxy) — download the Windows build, unzip, and run `Color Dash Galaxy.exe`.
>
> This repository contains the **source code and original project files**. Some of the art, audio and effects used during development came from third-party Asset Store packs that cannot be redistributed, so they are not included here (see [THIRD_PARTY_ASSETS.md](THIRD_PARTY_ASSETS.md)). The downloadable itch.io build is the way to play the game with all assets in place.

## Gameplay

You pilot a spaceship viewed from above in a field of space junk and hostile ships. Dodge, shoot, and constantly re-colour your ship to stay alive.

The colour rule is the heart of the game:

- Your ship can be **red, blue or yellow**, and you cycle through them at any time.
- Enemies and enemy projectiles of a **different** colour to your ship will destroy you on contact.
- Your bullets take the ship's current colour and only destroy enemies of the **same** colour.

Because the enemies that *can hit you* are exactly the ones you *can't shoot* (and vice versa), every moment is a quick read-and-react: switch to the right colour at the right time.

Design influences:
- **Touhou (Embodiment of Scarlet Devil)** — a tiny circular hitbox at the centre of the ship, so dense bullet patterns stay fair.
- **TKKN 99** — a bonus for dodging space junk at very close range.
- **Color Switch** — the colour-matching idea, but with free colour toggling instead of collectible-gated switches, to keep the pace fast.

### Enemies

- **Space junk** — drifts across the screen, alone or in rows; one shot to destroy.
- **Enemy ships** — fly in, stop, turn to face you, then fire spreads of projectiles at random angles.
- **Boss** — appears after 2:30. Made of three parts, each a random colour with its own health pool; destroy all three to win.

### Modes

Three difficulty levels (easy / normal / hard) plus an endless **survival mode**. Higher difficulty increases spawn rates, enemy speed, fire rate and boss health, and changes which enemies keep spawning once the boss arrives.

## Controls

| Key | Action |
| --- | --- |
| ← / → | Steer (rotate) the ship |
| ↑ / ↓ | Accelerate forward / backward |
| **Z** | Fire |
| **X** | Cycle ship colour (red → blue → yellow) |

The ship is driven with `Rigidbody2D` forces, so it carries inertia in both movement and rotation.

## Building from source

1. Install **Unity 2019.4.40f1** (the version this project was authored in).
2. Clone the repository and open the project folder in Unity Hub.
3. Some sprites, effects and audio are intentionally missing (see [THIRD_PARTY_ASSETS.md](THIRD_PARTY_ASSETS.md)). The project will open and compile, but those objects will show missing references in the editor. To play the complete game, use the itch.io build.
4. Open a scene from `Assets/Scenes/` (`Menu`, `PlayScene` or `Tutorial`) and press Play.

## Project structure

```
Assets/
├── Scripts/                 Game logic (C#)
│   ├── LevelManager.cs       Per-difficulty spawn parameters + spawn coroutine
│   ├── AudioManager.cs
│   ├── Player spaceship/     SpaceshipController, BulletManager, CloseDodgeDetector
│   ├── Enemy objects/        SpaceJunkManager, EnemySpaceshipManager, BossManager, IndividualBossPart
│   ├── UI/                   Menus, button handling, in-game HUD/timer
│   └── Tutorial/             Tutorial-scene behaviour
├── Prefabs/                 Player, bullets, enemies, boss, effects
├── Scenes/                  Menu, PlayScene, Tutorial
├── Shader/                  Damage-flash & grayscale shaders, URP pipeline assets
├── Arts/                    Animations, original space-junk art, Unity UI Samples
├── Audio/                   Music and sound effects
├── Plugins/                 DOTween
└── Resources/, Physics Material/
```

`LevelManager.cs` holds the spawn parameters for each difficulty in a dictionary (junk timing, spawn periods, enemy/boss speed, fire rate, boss health), and a `GameDifficulty` enum the enemy scripts read to pick the right values.

## Development notes

- ~22 weeks from concept to final build.
- Two rounds of user testing (10 testers each) drove balance and UX changes — for example: faster player movement and bullets, single-hit basic enemies, randomised enemy fire angles, separate music/SFX volume sliders, a gameplay timer, a transparency cue when overlapping same-colour enemies, and a randomised boss colour layout each run.

## License

Source code is released under the [MIT License](LICENSE). The MIT license covers **the code only** — third-party assets are not included in this repository and are governed by their own licenses (see [THIRD_PARTY_ASSETS.md](THIRD_PARTY_ASSETS.md)).
