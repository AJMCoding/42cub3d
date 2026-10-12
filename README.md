*This project has been created as part of the 42 curriculum by @fstark and @akortvel.*

# cub3D

## Description

**cub3D** is a graphics project inspired by *Wolfenstein 3D*, the game considered the
first First-Person Shooter in history. The goal is to build a simple 3D game engine
from scratch, using **ray-casting** techniques and the **MiniLibX** graphics library.

The program reads a scene description file (`.cub`), parses the map and its
configuration (wall textures, floor color, ceiling color, player position), and
renders a real-time, first-person 3D view of the maze. The player can move and look
around using the keyboard.

Main features of the mandatory part:
- Parsing and validation of `.cub` scene files (map + textures + colors).
- Real-time 3D rendering of the maze using ray-casting.
- Different textures depending on the wall orientation (North, South, East, West).
- Configurable floor and ceiling colors.
- Smooth player movement (`W`, `A`, `S`, `D`) and camera rotation (arrow keys).
- Clean exit on `ESC` or when closing the window.

Added features of the bonus part:
- Wall collisions.
- A minimap system.
- Doors which can open and close.
- Animated sprites.
- Rotate the point of view with the mouse.
- Better PC resource usage (the subject allowed access to the pc time only in the bonus part, so we could implement a maximum frame rate here)


## Instructions

### Requirements
- A Unix-like system (Linux / macOS).
- `cc` compiler and `make`.
- MiniLibX (system version or bundled sources).

### Compilation
```bash
make        # compiles the mandatory part
make bonus  # compiles the mandatory + the bonus part
make clean  # removes object files
make fclean # removes object files and the executable
make re     # fclean + make
make re_b   # fclean + make bonus
make run    # runs a simple bash script that lets you select the map you want to play from the mandatory maps
```

### Execution
#### Mandatory version
```bash
./cub3D path/to/map.cub
```
#### Bonus version
```bash
./cub3D_bonus path/to/bonusMap.cub
```
### Controls
| Key                                | Action                         |
|------------------------------------|--------------------------------|
| `W` `A` `S` `D`                    | Move through the maze          |
| `←` `→`, mouse movement (if bonus) | Look left / right              |
| `ESC`                              | Close the window and quit      |
| Window close (X)                   | Quit cleanly                   |

### Scene file (`.cub`) format
#### Mandatory
A scene file must define, in any order (except the map, which must come last):
- `NO`, `SO`, `WE`, `EA`: paths to the wall textures (North, South, West, East).
- `F`: floor color, as `R,G,B` (0-255 each).
- `C`: ceiling color, as `R,G,B` (0-255 each).
- The map itself, made only of `0` (empty space), `1` (wall) and `N`/`S`/`E`/`W`
  (player starting position and orientation). The map must be closed by walls.

Example:
```
NO ./textures/north.xpm
SO ./textures/south.xpm
WE ./textures/west.xpm
EA ./textures/east.xpm

F 220,100,0
C 225,30,0

111111
100101
101001
1100N1
111111
```
##### Bonus
a scene file must also define, in any order (except the map, which must come last):
- `DO`: path to the door texture.
- `SP`: path to the sprite texture.
- `A1` `A2`: path to the first and second frame of the animated sprite texture.

the map can now also include:
-  `D` (door) (with the limitation of having to be next to exactly 2 walls).
-  `P` (sprite)
-  `A` (animated sprite)

Example:
```
NO textures/wall_1.xpm
SO textures/wall_2.xpm
WE textures/wall_3.xpm
EA textures/wall_4.xpm
DO textures/bluestone.xpm
A1 textures/window_1.xpm
A2 textures/window_2.xpm
SP textures/bookshelve.xpm 
F 100,100,100
C 51,198,227

1111111111111111111111111111111111
10000000000000000000000000000000P1
11111101111D111100000A000000000011
100000100000001100000000000W000001
100000100010000D00P000000000000P01
1000000000010001000000000000000001
1101111111111111111111111111111111
100000001
100000001
111111111
```

## Resources

- [Lode's Computer Graphics Tutorial - Raycasting](https://lodev.org/cgtutor/raycasting.html) — the classic reference for implementing a DDA-based ray-casting engine.
- [MiniLibX documentation](https://github.com/42Paris/minilibx-linux) — official MiniLibX sources and usage notes.
- [Raycasting in C | 42 Cub3D] (https://www.youtube.com/watch?v=G9i78WoBBIU&t=116s)

### AI usage
AI was used to help design the initial project structure and to clarify
concepts around ray-casting math (DDA algorithm, wall-distance correction to avoid
fish-eye effect) during the planning phase. All code was tested and fully
understood by the authors; no AI-generated function was copy-pasted without review.
