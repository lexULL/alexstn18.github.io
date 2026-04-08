---
layout: project
title: "GHMTexTool"
summary: "Personal project for extracting and re-importing textures from PC ports of Grasshopper Manufacture games (Killer7, No More Heroes 1/2)"
image: /assets/images/ghm/logo.png
technologies: [Reverse Engineering, Modding, C++, Personal]
responsibilities:
  - Reverse-engineering custom file formats
  - Learning about the DDS image file format and about GCT0 (Nintendo's proprietary texture file format from the Wii)
duration: "1 month"
featured: true
--- 

[GitHub Link](https://github.com/lexULL/GHMTexTool)

GHMTexTool is a personal project born out of my interest in the games of GRASSHOPPER MANUFACTURE, the same studio whose visual style informed my NPR rendering research. The tool extracts and re-imports textures from the PC ports of Killer7, No More Heroes and No More Heroes 2: Desperate Struggle, targeting four proprietary archive formats: `.bin`, `.dat`, `.sti` and `.jmb`.

## How It Works

The core challenge was understanding undocumented binary file formats with no official documentation. Most of the format knowledge came from researching the Killer7 and No More Heroes modding community on Discord, where community members had already documented parts of the file structure and were willing to help fill in the gaps. Two existing open-source tools — SutandoTsukai181's No More Hashes gist and Venomalia's Dolphin Texture Extraction tool — also served as important references.

Extraction reads raw texture data out of the archives and writes it as standard DDS files. Re-importing reverses this, writing the modified DDS data back into the original archive at the correct offsets. A separate extraction mode generates MurmurHash-tagged filenames, placing the output directly into the format expected by Killer7's texture replacement folder for easy mod testing. For No More Heroes `.bin` GCT0 files specifically, a fix-and-hash pass strips 16 trailing empty bytes and applies the correct hash before converting to DXT1 DDS.

The tool is built with CMake and runs on both Windows and Linux.