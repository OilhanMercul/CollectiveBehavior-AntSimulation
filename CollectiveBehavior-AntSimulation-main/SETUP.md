# 🚀 Setup & Launch Guide — AntSimulation

This guide is intended for anyone who wants to run, explore, or observe the simulation.

It covers: compiling the project, launching it, understanding the available scenes, and tweaking simulation parameters.

> **Note:** Raylib 4.5 library files are already included in `lib/`. You only need to install a C++ compiler.

---

## What is this simulation?

This project simulates a swarm of ants modeled as physical particles in a 3D environment. Each ant is represented as a sphere with physical properties (mass, velocity, friction, adhesion). The collective behavior — pile formation, flow through funnels, bridge-building — emerges from local physics rules rather than explicit programming.

The simulation is built on **Position-Based Dynamics (PBD)**, the same technique used in real-time physics engines and game engines. Ants interact through:
- **Density constraints** — they resist being compressed, like a fluid
- **Distance constraints** — bonding forces that make them stick together
- **Friction & adhesion** — surface interactions with walls, floors, and 3D objects
- **Random locomotion** — individual ants randomly change direction, driving movement

> This project extends the original simulation by adding **pheromone-based trail formation**, where ants deposit chemical signals and steer toward higher concentrations — producing the characteristic trails observed in real Argentine ants.

---

## Project Structure

```
CollectiveBehavior-AntSimulation/
│
├── antsim.cpp                   # Entire simulation source code (~2700 lines, C++/Raylib)
├── settings.txt                 # Simulation parameters — edit this to change behavior
│
├── models/                      # 3D scene objects loaded at runtime
│   ├── funnel.glb               #   Scene 0: Funnel
│   ├── bracket.glb              #   Scene 1: Bracket
│   ├── plate.glb                #   Scene 2: Plate (crushing)
│   ├── coin.glb                 #   Scene 4: Coin Drop
│   └── tower.glb                #   Scene 5: Ant Tower
│
├── lib/                         # Pre-built Raylib 4.5 libraries for Windows 
│   ├── libraylib.a
│   ├── libraylibdll.a
│   └── raylib.dll
│
├── lighting.vs / lighting.fs    # GLSL shaders for scene lighting
├── lighting_instancing.vs       # Shader for rendering many particles efficiently
├── raylib.h / raymath.h         # Raylib API headers
├── rlgl.h / rlights.h           # Low-level rendering utilities
│
├── README.md                    # Project overview and academic context
└── SETUP.md                     # This file — setup and usage guide
```

> **The only files you need to edit** to change behavior are `antsim.cpp` (code) and `settings.txt` (parameters).

---

## Windows

### Step 1 — Install the compiler (w64devkit)

1. Download **w64devkit**: https://github.com/skeeto/w64devkit/releases
   - Get the latest `w64devkit-x64-x.xx.x.7z.exe`
2. Run it, it will unzip itself anywhere, e.g. `C:\w64devkit\`
3. Launch `w64devkit.exe` → a bash terminal opens

> If you already have **MSYS2** or **MinGW** with `g++` available, you can use them directly and skip to Step 2.

### Step 2 — Navigate to the project

In the w64devkit terminal:

```bash
cd "/c/Users/<YourName>/Documents/Cours/Collective Behavior/CollectiveBehavior-AntSimulation"
```

Verify you are in the right place:

```bash
ls
# You should see: antsim.cpp  lib/  models/  settings.txt  ...
```

### Step 3 — Compile

```bash
g++ antsim.cpp -Llib -lraylib -lopengl32 -lgdi32 -lwinmm -fopenmp -g -O2 -o antsim.exe
```

Compilation takes a few seconds. If successful, no error messages appear and `antsim.exe` is created.

**Compilation flags explained:**

| Flag | Category | Description |
|------|----------|-------------|
| `antsim.cpp` | Input | The source file to compile |
| `-Llib` | Library path | Tells the linker to look for libraries in the local `lib/` folder |
| `-lraylib` | Library | Links the Raylib graphics library (`lib/libraylib.a`) |
| `-lopengl32` | Library | Links the Windows OpenGL driver — required by Raylib for 3D rendering |
| `-lgdi32` | Library | Links the Windows GDI (Graphics Device Interface) — used by Raylib for window creation |
| `-lwinmm` | Library | Links the Windows Multimedia API — used by Raylib for audio and timers |
| `-fopenmp` | Parallelism | Enables OpenMP multi-threading, used to parallelize the particle simulation loop across CPU cores |
| `-g` | Debug | Embeds debug symbols in the binary (useful for debuggers like GDB) |
| `-O2` | Optimization | Applies level-2 compiler optimizations for better runtime performance without sacrificing stability |
| `-o antsim.exe` | Output | Sets the name of the generated executable |

> **Why `-Llib` and not a system path?** The Raylib library files are bundled directly in the `lib/` folder of this repo, so no system-wide installation is needed. The `-L` flag tells the linker where to find them locally.

### Step 4 — Run the simulation

```bash
./antsim.exe
```

> ⚠️ **Always launch from the terminal**, never by double-clicking. The program needs to be in its directory to find `models/` and `settings.txt`.

---

## macOS

### Step 1 — Install build tools

In a terminal:

```bash
xcode-select --install
```

### Step 2 — Get the macOS Raylib library

The `lib/libraylib.a` file included in this repo is compiled for **Windows**. On macOS, you need the macOS build:

1. Download `raylib-4.5.0_macos.tar.gz`: https://github.com/raysan5/raylib/releases/tag/4.5.0
2. Extract and copy `libraylib.a` into the project's `lib/` folder (replacing the existing file)

### Step 3 — Disable OpenMP

In `antsim.cpp`, comment out line 8:

```cpp
// #include <omp.h>
```

### Step 4 — Compile

```bash
clang++ -framework CoreVideo -framework IOKit -framework Cocoa -framework GLUT -framework OpenGL \
  lib/libraylib.a antsim.cpp -g -O2 -o antsim -std=c++11
```

### Step 5 — Run the simulation

```bash
./antsim
```

---

## Simulation Controls

| Key | Action |
|-----|--------|
| `SHIFT` | Toggle between 3D cursor mode and camera mode |
| `WASD` + `QE` | Move the 3D cursor around the scene (cursor mode) |
| `1` / `2` / `3` | Adjust cursor size (small / medium / large) |
| `WASD` + Mouse / Scroll | Move camera / Zoom (camera mode) |
| `IKJL` + `OU` | Resize the environment walls |
| `4` | Switch to next scene |
| `5` | Reset current scene |
| `6` / `7` | Start / stop recording particle positions to `frames.txt` |
| `8` / `9` | Start / stop recording FPS data to a `.csv` file |
| `M` | Print all particle positions to the terminal |


## Available Scenes

Press `4` to cycle through scenes. Press `5` to reset the current scene.

| # | Name | Description |
|---|------|-------------|
| 0 | **Funnel** | Ants pour through a funnel-shaped obstacle and disperse on the floor below |
| 1 | **Bracket** | Ants slowly fill three holes in a bracket structure, simulating bridging behavior |
| 2 | **Plate** | A flat plate descends and compresses a mass of ants (move with `Q`/`E`) |
| 3 | **Dispersal** | Open arena — ants disperse freely across the floor with no obstacles |
| 4 | **Coin Drop** | A coin falls and collides with a pile of ants |
| 5 | **Ant Tower** | Ants accumulate on a tower-shaped structure, crawling along its surface |
| 6 | **Crushed Ants** | A mass of ants is compressed from above |
| 7 | **Test Room** | Empty arena — used for pheromone trail experiments |

Each scene has its own physics parameters defined in `settings.txt`.

---

## Adjusting Parameters

All physics parameters are stored in [`settings.txt`](settings.txt) and are read at runtime — **no recompilation needed** to change them. Simply edit the file, then reset the simulation with `5`.

### Parameter reference

Each scene block follows this exact order (9 values after the scene name):

```
Scene Name          ← label only, not parsed
Viscosity           ← how much ants resist relative motion (fluid-like damping)
Distance Constraint Intensity  ← stiffness of bonds between ants (higher = stiffer)
Bond Split Distance ← how far apart two bonded ants can be before the bond breaks
                      (expressed as a multiplier of bond distance, e.g. 2.84 = 2.84×)
Max Number of Bonds ← maximum bonds per ant (integer, e.g. 3)
Surface Friction    ← friction between ants and walls/floor
Adhesive Strength   ← how strongly ants stick to walls and surfaces (0 = no adhesion)
Particle Friction   ← friction between individual ants colliding with each other
Timestep            ← simulation time step (smaller = more accurate, but slower)
Gravity             ← gravitational acceleration (higher = ants fall faster)
```

### Example — settings.txt excerpt

```
Funnel (scene 0)
0.408       ← Viscosity
0.0308      ← Distance Constraint Intensity
2.84        ← Bond Split Distance
3           ← Max Number of Bonds
0.024       ← Surface Friction
0.0000      ← Adhesive Strength (none for funnel)
0.1512      ← Particle Friction
0.01        ← Timestep
280.0       ← Gravity
```
## Troubleshooting

| Error | Fix |
|-------|-----|
| `cannot find -lraylib` | Check that `lib/libraylib.a` exists in the project |
| `cannot find -lopengl32` | Wrong compiler — use w64devkit or MinGW |
| Black window / instant crash | Launch from the terminal, not by double-clicking |
| OpenMP error | Try removing `-fopenmp` to test first |
| `g++ not found` | w64devkit is not running, or not in your PATH |

---

## Adjusting Parameters

Simulation parameters (viscosity, friction, adhesion, etc.) are configured in [`settings.txt`](settings.txt).  
The file contains detailed instructions for each parameter and each scene.
