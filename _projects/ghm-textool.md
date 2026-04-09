---
layout: project
title: "GHMTexTool"
summary: "Personal project for extracting and re-importing textures from PC ports of Grasshopper Manufacture games (Killer7, No More Heroes 1/2)"
description: "A command-line texture extraction and re-importing tool for the PC ports of Killer7 and No More Heroes 1/2, reverse engineering four proprietary archive formats with help from the modding community."
image: /assets/images/ghm/logo.png
tags: [Tools, Modding, Personal]
responsibilities:
  - Reverse-engineering custom file formats
  - Learning about the DDS image file format and about GCT0 (Nintendo's proprietary texture file format from the Wii)
duration: "1 month"
featured: true
order: 2
github: https://github.com/lexULL/GHMTexTool
---

The tool extracts and re-imports textures from the PC ports of Killer7, No More Heroes and No More Heroes 2: Desperate Struggle, targeting four proprietary archive formats: `.bin`, `.dat`, `.sti` and `.jmb`.

<center>
<figure style="flex: 1; margin-top: 0px; text-align: center;">
    <video controls style="border: 1px white solid; max-width: 100%;">
        <source src="{{ '/assets/images/ghm/EXAMPLE_OF_USAGE.mp4' | relative_url }}" type="video/mp4" />
    </video>
</figure>
</center>

## How It Works

The core challenge was understanding undocumented binary file formats with no official documentation. Most of the format knowledge came from researching the Killer7 and No More Heroes modding community on Discord, where community members had already documented parts of the file structure and were willing to help fill in the gaps. Two existing open-source tools — SutandoTsukai181's No More Hashes gist and Venomalia's Dolphin Texture Extraction tool — also served as important references.

Extraction reads raw texture data out of the archives and writes it as standard DDS files. Re-importing reverses this, writing the modified DDS data back into the original archive at the correct offsets. A separate extraction mode generates MurmurHash-tagged filenames, placing the output directly into the format expected by Killer7's texture replacement folder for easy mod testing. For No More Heroes `.bin` GCT0 files specifically, a fix-and-hash pass strips 16 trailing empty bytes and applies the correct hash before converting to DXT1 DDS.

The tool is built with CMake and runs on both Windows and Linux.

## GitHub Repository

[![GHMTexTool](https://gh-card.dev/repos/lexULL/GHMTexTool.svg)](https://github.com/lexULL/GHMTexTool)
