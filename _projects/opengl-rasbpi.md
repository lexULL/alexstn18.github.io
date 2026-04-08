---
layout: project
title: "OpenGLES Raspberry Pi Endless Runner"
summary: "University project through which I've learned the basics of 3D Graphics and compiling on Linux by making an infinite runner game"
image: /assets/images/rasbpi/logo.png
technologies: [Graphics Programming, 3D, C++, University]
responsibilities:
  - Learning the OpenGL Graphics API and about 3D rendering for the first time
  - Learning and applying 3D Math
  - Learning how to develop on Linux in a hardware-restrained environment
duration: "2 months"
---

[GitHub Link](https://github.com/lexULL/y1-pitfall3d)

I worked on this project for 8 weeks in Year 1. The game runs on a Raspberry Pi and was built entirely in C++ with OpenGL for rendering and Bullet Physics for collision and rigid body simulation.

## Rendering

3D static OBJ models are loaded and rendered through Assimp, following the LearnOpenGL model loading tutorial. The loader processes each node in the imported scene, extracts mesh vertex data and handles single and multi-texture models. Phong lighting is applied to both OBJ models and an animated MD2 model, implemented by following LearnOpenGL's lighting tutorials with additional shader optimizations needed to run acceptably on the Pi's hardware.

The Bullet Physics debug drawer is a custom OpenGL class that reads line data directly from the physics world and renders it to screen through its own vertex and fragment shaders, using a VAO/VBO pipeline. This made debugging collision shapes and broadphase issues significantly easier throughout development.

## Physics

A Bullet Physics dynamics world is set up with a full collision configuration, broadphase, dispatcher and constraint solver. The player character uses a capsule convex shape as its ghost object collision shape. A convex hull generation function was also added, capable of building collision shapes directly from a 3D model's mesh data for more accurate per-object collisions. Collision filtering is handled by overriding Bullet's collision dispatcher, allowing specific collision pairs to be selectively ignored.

## Gameplay and Procedural Generation

The level uses a chunk-based system, placing coins, obstacles and enemies at randomized positions based on the current seed. Difficulty increases progressively as the player collects coins, which raise the movement speed over time. Three difficulty presets are available from the menu, each with different run, jump and move speed values.

A random pronounceable word generator was implemented for procedural seeding, built around the CVC/VCV (consonant-vowel-consonant) alternation model. It generates a random word length between 4 and 10 characters, picks a starting letter, then alternates between consonants and vowels for each subsequent character based on a compile-time random seed.

## Menu and Game States

Input is handled through X11's event system, with key symbols stored and routed both to gameplay functions and forwarded to ImGui for menu navigation. A full game state backend drives a navigable menu with difficulty selection, a loading screen with 10 animated frames for level transitions, and an in-game pause state.

Notable features:
- Assimp model loading with multi-texture support
- Phong lighting on OBJ and MD2 models, optimized for Raspberry Pi
- Bullet Physics with capsule and convex hull collision shapes
- Custom Bullet debug drawer in OpenGL
- Chunk-based procedural level generation with scalable difficulty
- Pronounceable word generator using the CVC/VCV model
- ImGui menu system with game state management and animated loading screen
- X11 input handling routed to both gameplay and ImGui