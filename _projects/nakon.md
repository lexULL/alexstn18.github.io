---
layout: project
title: "Nakon"
summary: "CoD:Zombies-inspired game in a FPS custom engine from scratch running on PC and PS5"
description: "A Call of Duty: Zombies-inspired FPS built on a custom cross-platform engine over 4 months, covering engine systems in the first half and game development with artists in the second. Available on itch.io."
image: /assets/images/nakon/nakon-demo.gif
technologies: [Custom Engine, 3D, C++, University]
responsibilities:
  - Scene Manager implementation giving the engine support for handling of multiple scenes
  - Designed and programmed the in-game UI
  - Designed and programmed in-editor tools for (and together with) artists
  - Was a core part of helping to improve the "juicyness" of the game
  - Handling of CI/CD tasks
  - Working on Marketing assets (e.g. screenshots, trailer)
duration: "4 months"
team_size: "12 people"
featured: true
---

The first two months were spent building engine systems, and the final two months on shipping the game alongside a team of artists. The game is available on [itch.io](https://buas.itch.io/nakon).

## Building the Engine

The engine is built on top of BEE, a provided framework, and targets both PC and PS5. My contributions covered cross-platform support, asset pipelines, serialization and scene management.

I started with a Blender add-on that lets designers tag meshes with custom metadata. These tags get embedded into exported `.gltf` files and parsed by the engine, allowing each mesh to be interpreted differently — for example, distinguishing walkable surfaces from interactable objects — without any manual per-asset setup in code.

Getting the project compiling and running on PS5 in both Debug and Release was a major milestone. I cleaned up non-portable GLFW calls from the character controller and integrated BEE's cross-platform input mapping system, making the game fully playable on the devkits with a PS5 controller.

For serialization I designed a templated `Serializable<T>` CRTP base class, so any config struct can expose `Serialize()` and `Deserialize()` with no boilerplate. This was adopted across the codebase for player settings, camera FOV, navmesh configs and more. To fix slow startup times caused by navmesh recomputation on every launch, I also implemented binary navmesh caching — cutting load times significantly on large maps.

The scene manager was my most involved engine task. It supports runtime scene registration, switching and resetting, with deferred cleanup to avoid crashes from systems accessing destroyed resources mid-frame. The main challenge was that some engine systems depended on entities that got destroyed during transitions. I solved this by introducing core systems — persistent systems excluded from scene cleanup — and adding a `TryGetSystem<>()` call to the ECS backend after teammates were crashing by assuming systems still existed post-transition.

Notable engine features I built:
- Blender mesh tagging pipeline with in-engine preview
- Cross-platform PS5 compilation and controller input
- Templated serialization base class with JSON and binary support
- Binary navmesh caching for fast startup
- Scene manager with queued cleanup, core systems and PS5 support

## Making the Game

In the second block we shifted to shipping the game with artists. I focused on the FPS camera, the full UI layer and various engine improvements.

I reworked the camera around a state machine with FPS, free roam and death states. Camera effects like view bobbing, FOV scaling, camera shake and a death drop are ECS components on the camera entity, so they can be toggled without touching the core update logic. The raw camera transform is stored separately from the visual one, which let the weapon attachment system follow the unaffected position and avoid the weapon shaking with the camera.

For the final sprint I was on the UI strike team, implementing all menus and in-game HUD using the Firefly custom UI system. This included a navigable main menu with a cinematic background and controller support, BUas and FMOD splash screens with fade in/out and a skip button, a credits screen, and a full in-game HUD with lerped health and ammo bars, score popups with colour coding and a drop pickup display supporting up to three simultaneous pickups with dynamic positioning. All of it was built against artists' mockups and iterated on with feedback from the team and teachers.

Notable game features I built:
- State-based FPS camera with modular ECS effect components
- Weapon attachment system supporting two independent hand models
- Full UI layer: menu, splash screens, credits and in-game HUD
- Weapon and menu audio integration
- ImGui toast notifications and editor UI toggle for the art team

Later during the project, our team presented the game at a playday and an industry showcase. I helped edit the trailer and took the marketing screenshots published on our itch page.