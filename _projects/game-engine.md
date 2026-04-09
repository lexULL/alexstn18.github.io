---
layout: project
title: "Game Engine Assignment"
summary: "University assignment of creating a game engine with ImGui, particle system, glTF loader and tile-based level editor running on PC and compiling on PS5"
description: "A custom game engine built as a static library in C++, featuring an EnTT-based particle system, glTF model loading with node hierarchies, a runtime resource manager and a tile-based level editor with serialization support."
image: /assets/images/game-engine/game-engine-logo.gif
tags: [Engine, Tools, University]
responsibilities:
  - Set up cross-platform compilation for PC and PS5
  - Develop a particle system using the EnTT ECS library
  - Build an ImGui-based editor layer with gizmo support
  - Implement glTF model loading with node hierarchies
  - Build a runtime resource manager with reference counting
  - Implement serialization and deserialization of levels and particle emitters
  - Develop a tile-based level editor with mouse-based selection
duration: "2 months"
order: 10
---

## Building the Engine

The engine is structured as a static library linked to a demo application, with systems organized around EnTT's entity-component-system. Core systems include a particle system, a runtime resource manager, and a level editor.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/game-engine/particle_demo.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

The particle system manages emitters and particles as EnTT entities, with components controlling emission rate, lifetime, size, velocity, and cone direction. Emitters are fully controllable from the ImGui editor layer and can be serialized to and loaded from JSON using the Cereal library.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/game-engine/gltf.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

For model loading, I built a glTF loader on top of tinygltf that traverses node hierarchies, binding mesh and texture data to ECS entities with Transform and HierarchyComponent components. The resource manager wraps this loader with a shared pointer cache and reference counting, following the Rule of Five for correct runtime resource management.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/game-engine/leveleditor.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

The level editor allows placing glTF models on a tile grid via ray–AABB intersection, with ImGuizmo gizmos for translation, rotation and scale, grid snapping via Left Ctrl, and full serialization of the scene to JSON.

## Notable Features

- Fixed and dynamic timestep with pause and timescale control
- Particle system with multiple emitter types, cone visualization, and mesh swapping via file browser
- ImGui viewport with docking, emitter controls, and a file browser extension
- glTF loading with transform hierarchies and per-model bounding boxes
- Runtime resource manager with reference counting and Rule of Five
- Tile-based level editor with mouse selection, gizmo manipulation, and scene serialization
- Zero compiler warnings at warning level 4, with static analysis applied throughout