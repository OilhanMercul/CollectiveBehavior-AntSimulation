# 🚀 Setup & Launch Guide — AntSimulation

This guide explains how to compile and run the simulation on **Windows** and **macOS**.

> **Note:** Raylib 4.5 library files are already included in `lib/`. You only need to install a C++ compiler.

---

## Windows

### Step 1 — Install the compiler (w64devkit)

1. Download **w64devkit**: https://github.com/skeeto/w64devkit/releases
   - Get the latest `w64devkit-x.xx.x.zip`
2. Unzip it anywhere, e.g. `C:\w64devkit\`
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
| `SHIFT` | Toggle between 3D cursor and camera |
| `WASD` + `QE` | Move the 3D cursor around the scene |
| `1` / `2` / `3` | Adjust cursor size |
| `WASD` + Mouse / Scroll | Move camera / Zoom |
| `IKJL` + `OU` | Resize environment walls |
| `4` | Switch scene |
| `5` | Reset simulation |
| `6` / `7` | Start / stop frame data recording |
| `8` / `9` | Start / stop FPS/performance recording |

**Available scenes:** Funnel, Bracket, Plate, Dispersal, Coin Drop, Ant Tower, Crushed Ants

---

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
