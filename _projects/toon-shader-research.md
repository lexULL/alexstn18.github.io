---
layout: project
title: "Non-photorealistic Rendering Research in UE5"
summary: "Project for researching non-photorealistic rendering styles — project uses Unreal Engine 5 as a framework"
description: "A research project into non-photorealistic rendering, resulting in a cartoon/cel shading post-process effect combined with an Anisotropic Kuwahara Filter implemented in Unreal Engine 5's material system."
image: /assets/images/toon/logo.png
technologies: [Graphics Programming, Unreal Engine, Research, Self-Study]
responsibilities:
  - Researched non-photorealistic rendering styles from different games (e.g. Cartoon Shading, Kuwahara Filter)
  - Implemented researched rendering styles into Unreal Engine
duration: "32 total hours"
---

## Research and State of the Art

The initial direction was a watercolor shader inspired by the painterly portrait style of Disco Elysium, but that proved too technically ambitious given my skill level at the time. I settled on harsh-edge cartoon/cel shading as the state of the art instead, drawing inspiration from GRASSHOPPER MANUFACTURE's visual style in games like killer7 and No More Heroes. To push it closer to the original artistic goal, I added an Anisotropic Kuwahara Filter on top — a painterly image abstraction filter — to give the effect a more expressive, hand-painted quality.

The research process involved reading papers, articles and interviews and surveying games with distinctive non-photorealistic styles over the course of several weeks.

## Implementation

Rather than prototyping in ShaderToy or a separate OpenGL project, I went directly into Unreal Engine 5, which I had no prior material shader experience with at the time. This was a deliberate choice to learn Unreal's Material Blueprint node system and understand how post-processing is handled in a production engine — something I was curious about after seeing games like Hi-Fi Rush ship cartoon rendering in Unreal Engine 4.

The cel shading was implemented through Unreal's post-process material nodes. The Kuwahara Filter was written almost entirely from scratch in HLSL, based on research papers I read during the earlier stages. This was my first time writing HLSL, though the transition from GLSL was manageable.

All parameters were exposed as editable material variables so that any team member could tweak the effect's intensity and behavior without touching the shader code. In practice the effect was integrated into the pause menu rather than the full game, as the artists were concerned it would conflict with the in-game art style — a smaller scope than planned, but it shipped.

## Reflection

Starting the proof of concept directly in Unreal rather than in an isolated environment was both the biggest risk and the biggest payoff of this project. It forced me to learn Unreal's material system quickly and gave me a real understanding of how post-processing pipelines work in a commercial engine. Writing the Kuwahara Filter from papers rather than an existing implementation was the most technically satisfying part of the process, and it directly influenced how I approached the same filter later in my Godot plugin.