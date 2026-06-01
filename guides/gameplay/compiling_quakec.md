---
title: Compiling QuakeC
---

The compiler is in `compiler/`. It takes the `.qc` source files in `quake-src/` and outputs `progs.dat`.

## Windows

Extract `compiler/ftetools_win64.zip`. Inside you'll find:

- **`fteqccgui64.exe`**  -  GUI IDE with editor and one-click compile. Recommended for the workshop.
- **`fteqcc64.exe`**  -  command-line compiler.

**Using the GUI:** Open `fteqccgui64.exe`, go to **File > Open** and open `quake-src/qcsrc/progs.src`. Click Compile. The output goes directly to `quake/workshop/progs.dat`.

**Using the CLI:**
```
fteqcc64.exe -src quake-src\qcsrc\
```

## Linux

`compiler/ftetools_linux-x64/fteqcc64`  -  run directly, no extraction needed.

```bash
./compiler/ftetools_linux-x64/fteqcc64 -src quake-src/qcsrc/
```

## Output

After a successful compile, `progs.dat` is written directly to `quake/workshop/progs.dat`. No copy step needed.

Launch: `engine/ironwail -game workshop`

## Compile errors

FTEQCC prints errors with file and line number. Fix the error, recompile. A clean compile ends with a line like `X statements, Y seconds`.
