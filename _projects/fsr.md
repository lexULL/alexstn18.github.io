---
layout: project
title: "Flower, Sun & Rain (PS2) Texture Extraction"
summary: "Short personal project for learning how the PlayStation 2 stored and loaded textures"
image: /assets/images/fsr/fsr-logo.png
technologies: [Reverse Engineering, C++, Personal]
responsibilities:
  - Learned about the PS2's Graphics Synthesizer and the way it stores/loads textures
duration: "1 day"
---

This tool extracts textures from the PS2 version of Flower, Sun and Rain, a lesser-known GRASSHOPPER MANUFACTURE adventure game. Like my earlier work on GHMTexTool, this project was driven by an interest in the studio's back catalogue and a curiosity about how their older games store and encode image data. The starting point for understanding the FSR file format came from community member Bigmanjapan, who explained how files are structured in the game and pointed me toward the official PlayStation 2 Graphics Synthesizer User's Manual as the primary reference for the texture and CLUT formats.

## How It Works

The tool operates in two modes. The first scans a folder of `.BIN` archive files, searches for known magic byte sequences that mark the beginning of image and CLUT blocks, and extracts the raw indexed pixel data and palette data into separate `.img` and `.clut` files. Width and height are read from a fixed offset relative to the magic bytes. The tool distinguishes between 8bpp and 4bpp texture formats based on which magic byte pattern precedes each block, though only 8bpp is fully supported at this stage.

The second mode takes those extracted files and converts them into TGA images. The PS2 stores colour palettes in a scrambled CLUT layout where groups of 8 palette entries are interleaved in a non-linear order across 8 row pairs. A reordering pass unscrambles this layout before the indexed pixel data is looked up against it. Alpha values below 128 are scaled by 2 to match the PS2's half-range alpha convention, and the image is vertically flipped on write since PS2 textures are stored bottom-up.

The CLUT reordering algorithm was worked out with help from a peer who helped figure out the PS2 CLUT table arranging logic.