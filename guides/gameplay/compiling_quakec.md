---
title: Compiling QuakeC
---

The compiler is in `tools/compiler/`. It takes the `.qc` source files in `resources/quake-src/` and outputs `progs.dat`.

## Windows

Extract `tools/compiler/ftetools_win64.zip`. Inside you'll find:

- **`fteqccgui64.exe`**  -  GUI IDE with editor and one-click compile. Recommended for the workshop.
- **`fteqcc64.exe`**  -  command-line compiler.

**Using the GUI:** Open `fteqccgui64.exe`, go to **File > Open** and open `resources/quake-src/qcsrc/progs.src`. Click Compile. The output goes directly to `resources/quake/workshop/progs.dat`.

**Using the CLI:**
```
fteqcc64.exe -src resources\quake-src\qcsrc\
```

## Linux

`tools/compiler/ftetools_linux-x64/fteqcc64`  -  run directly, no extraction needed.

```bash
./tools/compiler/ftetools_linux-x64/fteqcc64 -src resources/quake-src/qcsrc/
```

## macOS

Extract `tools/compiler/fteqcc_macOS_universal.zip`. Inside you'll find:

- **`fteqcc`**  -  universal binary, works on both Apple Silicon and Intel.

```bash
./tools/compiler/fteqcc -src resources/quake-src/qcsrc/
```

## Output

After a successful compile, `progs.dat` is written directly to `resources/quake/workshop/progs.dat`. No copy step needed.

Launch: `tools/engine/ironwail -basedir resources/quake -game workshop`

## Compile errors

FTEQCC prints errors with file and line number. Fix the error, recompile. A clean compile ends with a line like `X statements, Y seconds`.
