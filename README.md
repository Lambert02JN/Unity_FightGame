# Unity_FightGame

**A first-person multiplayer combat prototype built with Unity 2018.3.14f1 and C#.**

[View the source code](https://github.com/Lambert02JN/Unity_FightGame)

## Overview

Unity_FightGame explores the programming behind a small networked combat game. The custom scripts handle local-player setup, cannonball firing, networked projectile spawning, projectile cleanup, and a hit response that returns the affected player to a spawn position. The project uses Unity's legacy `UnityEngine.Networking` API and Unity Standard Assets for first-person movement.

This portfolio entry focuses on **my C# programming work**. The characters, animations, artwork, and other imported assets are third-party assets and are **not my original creations**.

## Controls

The first-person controller uses Unity's default input mappings:

| Input | Action |
| --- | --- |
| `W` `A` `S` `D` | Move |
| Mouse | Look around |
| Left mouse button (`Fire1`) | Fire a cannonball |
| `Space` (`Jump`) | Jump |
| Left `Shift` | Run |

When a cannonball hits a player, the hit-response script moves that player back to a spawn position and plays a sound. Cannonballs are removed by the server after a short lifetime (default: two seconds).

## Programming highlights

- **Networked firing:** `CannonController.cs` accepts fire input from the local player, asks the server to create a cannonball, applies force in the camera's forward direction, and spawns the projectile for connected clients.
- **Projectile lifetime:** `CannonballController.cs` counts the projectile's age on the server and destroys it when it expires.
- **Hit response:** `DamageScript.cs` detects collisions with objects tagged `Ball` and uses a network message to resolve the hit, return the local player to a spawn position, and play audio.
- **Player setup:** `PlayerController.cs` contains the first-person controller, camera, and audio-listener setup for networked player objects.

## Project files

| File | Purpose |
| --- | --- |
| [`Assets/Scripts/CannonController.cs`](Assets/Scripts/CannonController.cs) | Fire input and networked projectile spawning |
| [`Assets/Scripts/CannonballController.cs`](Assets/Scripts/CannonballController.cs) | Server-side projectile lifetime |
| [`Assets/Scripts/DamageScript.cs`](Assets/Scripts/DamageScript.cs) | Collision and hit response |
| [`Assets/Scripts/PlayerController.cs`](Assets/Scripts/PlayerController.cs) | Networked player component setup |

## Running the project

1. Open the project in **Unity 2018.3.14f1**.
2. Open `Assets/Scenes/SampleScene.unity` and inspect the scene and required network/player setup before pressing Play.

**Repository status:** The committed `SampleScene` contains only a camera and directional light. It does not contain the player and network-manager setup needed to demonstrate the scripted combat flow directly. Also, the current `PlayerController.cs` disables the first-person controller, camera, and audio listener without checking whether the object belongs to the local player. The controls above describe the intended input implemented in the scripts; the repository should be completed and play-tested before presenting it as a playable build.

## Contribution and asset attribution

**My contribution:** I wrote the four C# scripts in `Assets/Scripts/` that implement the gameplay and networking behaviour described above.

**Third-party materials:** The characters, character animations, visual artwork, and imported Unity assets were sourced from asset packages. The `Assets/Standard Assets/` scripts are Unity Standard Assets, not my code. Credit and licenses for any other imported packages should be added from their original package documentation before redistribution.

This project is included in my portfolio as a **technical programming sample**, with the authorship of its visual assets stated separately.
