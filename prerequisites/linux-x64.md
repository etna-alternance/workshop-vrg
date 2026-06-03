# Prerequisites — Linux x86-64

## TrenchBroom

TrenchBroom 2025.4 requires **Qt 6.7 or later**. Install it via your package manager if not already present:

```bash
# Debian / Ubuntu
sudo apt install libqt6core6 libqt6gui6 libqt6widgets6 libqt6opengl6

# Fedora
sudo dnf install qt6-qtbase
```

TrenchBroom is distributed as an AppImage — make it executable and run it directly:

```bash
chmod +x tools/map_editor/TrenchBroom-Linux-x86_64-v2025.4-Release.AppImage
./tools/map_editor/TrenchBroom-Linux-x86_64-v2025.4-Release.AppImage
```

## ericw-tools

No special dependencies. Extract `tools/map_editor/ericw-tools-v0.18.1-Linux.zip` and run the binaries directly.

## Ironwail

No special dependencies beyond standard OpenGL/SDL2 libraries, which are present on most desktop Linux installs.
