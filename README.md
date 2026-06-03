# cub3D

> [日本語版はこちら](README_ja.md)

A 3D maze renderer built with raycasting, inspired by [Wolfenstein 3D](https://en.wikipedia.org/wiki/Wolfenstein_3D).
This is a project from the [42 Tokyo](https://42tokyo.jp/) curriculum.

## Overview

cub3D renders a first-person view of a maze defined by a `.cub` map file. It uses the [DDA (Digital Differential Analyzer)](https://lodev.org/cgtutor/raycasting.html) algorithm to cast rays and draw textured walls with correct perspective.

### Features

- Real-time raycasting with textured walls
- Configurable wall textures (N/S/E/W) via XPM files
- Customizable floor and ceiling colors
- Smooth player movement (W/A/S/D) and rotation (arrow keys)
- Map validation (wall enclosure, valid characters, single player spawn)
- Cross-platform support (Linux / macOS)

## Getting Started

### Prerequisites

- `cc` (C compiler with C99 support)
- `make`
- Linux: X11 libraries (`libXext`, `libX11`)
- macOS: Xcode Command Line Tools

### Build & Run

The MiniLibX graphics library is automatically cloned during the build:
- **macOS**: [minilibx_macos](https://github.com/ncoden/minilibx_macos.git)
- **Linux**: [minilibx-linux](https://github.com/42Paris/minilibx-linux.git)

```sh
make
./cub3d <map_file.cub>
```

Example:

```sh
./cub3d map/valid/lodev.cub
```

### Controls

| Key | Action |
|-----|--------|
| `W` | Move forward |
| `S` | Move backward |
| `A` | Strafe left |
| `D` | Strafe right |
| `←` | Rotate left |
| `→` | Rotate right |
| `ESC` | Quit |

## Map Format

Map files use the `.cub` extension:

```
NO ./textures/north.xpm
SO ./textures/south.xpm
WE ./textures/west.xpm
EA ./textures/east.xpm

F 120,120,120
C 200,220,255

111111
1N0001
100001
100001
100001
111111
```

- `NO/SO/WE/EA` — wall textures for each cardinal direction
- `F` / `C` — floor / ceiling RGB colors
- Map characters: `1` = wall, `0` = floor, `N/S/E/W` = player start position and direction
- The map must be fully enclosed by walls

## Project Structure

```
.
├── main.c                  # Entry point
├── cub3d.h                 # Main header and data structures
├── srcs/
│   ├── parser.c            # Map file parsing
│   ├── check.c             # Config validation
│   ├── check_map.c         # Map wall enclosure validation
│   ├── find_player.c       # Player spawn detection
│   ├── init.c              # Initialization and texture loading
│   ├── cub3d.c             # Core setup and cleanup
│   ├── utils.c             # Utility functions
│   ├── debug.c             # Debug output
│   ├── dda/
│   │   ├── dda.c           # Raycasting (DDA algorithm)
│   │   ├── dda_utils.c     # Pixel drawing and ray initialization
│   │   └── texture.c       # Texture loading and pixel sampling
│   └── hooks/
│       ├── hooks.c         # Render loop and window events
│       └── key_hook.c      # Keyboard input and player movement
├── libft/                  # Custom C standard library
├── textures/               # XPM texture files
└── map/
    ├── valid/              # Valid test maps
    └── invalid/            # Invalid test maps
```

## Authors

- [Natsumi Teshima](https://github.com/Killua0615)
- [Yuki Wada](https://github.com/kitopito)
