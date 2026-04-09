---
layout: project
title: "Pitfall Remake"
summary: "Remake of the Atari 2600 classic Pitfall in a software-rendered C++ template as a university project"
description: "A 2D remake of the Atari 2600 classic built on a software renderer template, featuring rope physics, tile-based collision, parallax scrolling, a CRT post-process shader and persistent JSON save/load."
image: /assets/images/pitfall/logo.png
tags: [Game, University]
responsibilities:
  - Learned about using tile-sheets for 2D games for the first time
  - Learned how to develop a complex C++ program without relying on STL
  - Learned how to document my learning processes
duration: "2 months"
order: 13
---

[GitHub Link](https://github.com/lexULL/y1-pitfall)

## Physics and Movement

The rope is simulated by calculating each segment's position using sine and cosine based on the current swing angle. While attached to the rope, the player's position is locked to a hitbox formed around the rope's lowest segment, keeping the attachment visually consistent as the rope swings. Camera movement is smoothed using linear interpolation — the desired offset is calculated each frame and lerped toward the current offset, scaled by delta time to keep it framerate independent.

Coordinate systems in the game are world, local and screen. Entities are positioned in world space, hitboxes are calculated in local space relative to each actor's own position and dimensions, and world-to-screen conversion happens at render time by subtracting the camera offset from each object's position.

## Collision

Tile-based AABB collision was implemented by only testing tiles in the immediate vicinity of the player rather than the full tilemap, keeping the collision checks efficient. AABB is also used for player interactions with ropes, crocodiles, scorpions and the shrinking and growing holes. Circle-to-square collision was researched during development as an additional learning point, though the final game uses AABB throughout.

## Optional Features

Parallax scrolling is achieved by drawing the background layer with the camera offset multiplied by 0.5, creating a sense of depth without any additional geometry. A zoom effect was implemented by rendering all game assets to an intermediate sprite and then drawing that sprite to screen scaled by a zoom factor using `DrawScaled`.

The CRT shader and vignette were implemented in GLSL with help from a peer who taught me how to write shaders and explained how scanlines and vignette approximations work. The vignette uses vector normalization to more accurately approximate screen bounds. Both effects run as a post-process pass over the final frame.

JSON parsing was integrated through a library set up with peer help, used both for reading game data and for the save and load system. Checkpoints are written to a JSON file on disk and persist between runs, so the player can continue from the last reached checkpoint on the next session.

Notable features:
- Rope simulation with sine/cosine swing and player attachment
- Lerp-based smooth camera with delta time scaling
- Tile-vicinity AABB collision for player and all entities
- Parallax scrolling background layer
- Zoom in/out via scaled intermediate render target
- CRT scanlines and vignette GLSL post-process shader
- JSON parsing for game data and persistent checkpoint save/load