---
layout: project
title: "Nakon"
summary: "CoD:Zombies-inspired game in a FPS custom engine from scratch running on PC and PS5"
description: "A Call of Duty: Zombies-inspired FPS built on a custom cross-platform engine over 4 months, covering engine systems in the first half and game development with artists in the second. Available on itch.io."
image: /assets/images/nakon/nakon-demo.gif
tags: [Engine, Game, Team, University]
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

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/nakon/blender_pipeline.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

I started with a Blender add-on that lets designers tag meshes with custom metadata. These tags get embedded into exported `.gltf` files and parsed by the engine, allowing each mesh to be interpreted differently — for example, distinguishing walkable surfaces from interactable objects — without any manual per-asset setup in code.

Getting the project compiling and running on PS5 in both Debug and Release was a major milestone. I cleaned up non-portable GLFW calls from the character controller and integrated BEE's cross-platform input mapping system, making the game fully playable on the devkits with a PS5 controller.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/nakon/serialization.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

For serialization I designed a templated `Serializable<T>` CRTP base class, so any config struct can expose `Serialize()` and `Deserialize()` with no boilerplate. This was adopted across the codebase for player settings, camera FOV, navmesh configs and more. To fix slow startup times caused by navmesh recomputation on every launch, I also implemented binary navmesh caching — cutting load times significantly on large maps.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/nakon/scene_manager.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

The scene manager was my most involved engine task. It supports runtime scene registration, switching and resetting, with deferred cleanup to avoid crashes from systems accessing destroyed resources mid-frame. The main challenge was that some engine systems depended on entities that got destroyed during transitions. I solved this by introducing core systems — persistent systems excluded from scene cleanup — and adding a `TryGetSystem<>()` call to the ECS backend after teammates were crashing by assuming systems still existed post-transition.

Notable engine features I built:
- Blender mesh tagging pipeline with in-engine preview
- Cross-platform PS5 compilation and controller input
- Templated serialization base class with JSON and binary support
- Binary navmesh caching for fast startup
- Scene manager with queued cleanup, core systems and PS5 support

## Making the Game

In the second block we shifted to shipping the game with artists. I focused on the FPS camera, the full UI layer and various engine improvements.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/nakon/camera_showcase.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

I reworked the camera around a state machine with FPS, free roam and death states. Camera effects like view bobbing, FOV scaling, camera shake and a death drop are ECS components on the camera entity, so they can be toggled without touching the core update logic. The raw camera transform is stored separately from the visual one, which let the weapon attachment system follow the unaffected position and avoid the weapon shaking with the camera.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/nakon/finalcamera.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

For the final sprint I was on the UI strike team, implementing all menus and in-game HUD using the Firefly custom UI system. This included a navigable main menu with a cinematic background and controller support, BUas and FMOD splash screens with fade in/out and a skip button, a credits screen, and a full in-game HUD with lerped health and ammo bars, score popups with colour coding and a drop pickup display supporting up to three simultaneous pickups with dynamic positioning. All of it was built against artists' mockups and iterated on with feedback from the team and teachers.

Notable game features I built:
- State-based FPS camera with modular ECS effect components
- Weapon attachment system supporting two independent hand models
- Full UI layer: menu, splash screens, credits and in-game HUD
- Weapon and menu audio integration
- ImGui toast notifications and editor UI toggle for the art team

Later during the project, our team presented the game at a playday and an industry showcase. I helped edit the trailer and took the marketing screenshots published on our itch page.

## Working in the Team

The project ran across four sprints using a strike team structure, where each programmer was assigned to a focused area per sprint rather than working across the whole codebase at once. I contributed to the pipelines, 3Cs, audio and UI strike teams across the four sprints. Following the strike team structure properly in the final sprint — something we had struggled with earlier — was one of the reasons Sprint 4 was the most productive one.

At the end of Sprint 3 I suggested we gather in the lab to test the build together before planning Sprint 4. We played through it as a group, collected a list of issues on the spot and used that directly to form the Sprint 4 strike teams and reprioritize accordingly. It turned out to be one of the more useful sessions of the project.

The UI work in the final sprint involved constant back-and-forth with the two artists on the team. I built everything against their mockups and checked back with them regularly as I iterated, making sure the implementation matched what they intended visually and that they could still modify assets without breaking anything on the code side. Feedback from a teacher on the UI also shaped a lot of the final polish — the cinematic menu background, the splash screens and the score popup effects all came out of those conversations.

I also reviewed pull requests consistently throughout all four sprints and filed bug reports on the GitHub Projects board whenever I found issues during testing, including reproduction steps for anything non-obvious.
