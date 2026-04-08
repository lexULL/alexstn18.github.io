---
layout: project
title: "Godot Stylized Shaders Plugin"
summary: "Self-study project for learning post-processing effects and for learning the Godot Engine, using GDExtension"
description: "A public Godot Engine plugin written in C++ via GDExtension, providing a suite of stackable stylized post-process effects with a customizable editor UI. Submitted to the Godot Asset Library."
image: /assets/images/godot/godot-demo.gif
tags: [Rendering, Tools, Self-Study]
responsibilities:
  - Learning how to use the Godot Engine for the first time
  - Learning about Compositor Effects in Godot Engine, the engine's modern alternative to "gdshader"s that run as compute shaders instead
  - Learning about post-processing effects and their implementation
  - Learning how to make user-friendly UI for a tool/plugin
duration: "2 months"
---

The plugin is publicly available on [GitHub](https://github.com/alexstn18/godot-stylized-shaders-plugin) and was submitted to the Godot Asset Library at the end of the block.

## Building the Plugin

The plugin is built with Godot's GDExtension API in C++, using compute shaders written in GLSL for all post-process effects. This was my first time working with a large external framework in C++, and a significant part of the early weeks was spent understanding Godot's rendering pipeline, its class registration macros and how to bridge C++ code with the editor.

The core of the architecture is a `BaseShader` abstract class that handles the compute pipeline boilerplate — initializing the render device, managing uniforms, dispatching the compute list and cleaning up. Each effect inherits from this and only needs to define its push constant data and shader logic. This made adding new effects straightforward and kept the individual shader classes lean.

To handle push constant alignment issues (a recurring pain point when sending data to the GPU), I parameterized each shader's uniforms through the push constant buffer and wrapped the data in a typed container class to avoid exposing raw byte arrays throughout the codebase. I also added support for user-supplied `Callable` functions that get executed within the compute loop, giving users a hook to extend any effect without subclassing it.

For the multi-pass effects — HDR Bloom and the Anisotropic Kuwahara Filter — I had to manage intermediate render targets between passes manually, since Godot's pipeline doesn't allow reading and writing to the same texture in one dispatch. The Kuwahara filter also required downsampling and upsampling passes to hit acceptable performance, plus NaN checks in the shader to correct weighting artifacts.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/godot/pres.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

Notable shaders implemented:
- Outline shader with customizable width, color and animated jitter
- CRT shader with scanlines and vignette
- VHS shader with animated scanlines, screen grain and a vertical distortion bar
- Bayer dithering shader
- Pixelization shader
- HDR Bloom (multi-pass)
- Anisotropic Kuwahara Filter (multi-pass with downsampling)
- Posterization and invert color shaders

## Editor UI

The plugin UI lives inside a custom editor panel built entirely in C++, loading its layout from a Godot scene file at runtime. Effects can be toggled individually, stacked in any order and reordered at runtime — with full undo/redo support through Godot's `UndoRedo` manager. Each effect exposes its parameters through sliders and color pickers that update the push constant buffer live.

To reduce boilerplate when constructing UI nodes from C++, I implemented a `NodeBuilder` helper class using the builder pattern — suggested by a teacher during a 1-on-1. This significantly cleaned up the UI construction code and became one of the more useful patterns I picked up this block.

## DevOps and Publishing

I set up a GitHub Actions workflow based on the official `godot-cpp-template`, building the plugin binaries for Windows, Linux and macOS across Debug and Release configurations on every push. I also configured clang-tidy for static analysis and generated XML documentation for all exposed classes using Godot's GDExtension docs system.

The plugin was submitted to the Godot Asset Library in Week 8 and the repository includes a README with a demo video, build instructions and a full feature list.