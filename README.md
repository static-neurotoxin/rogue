# Rogue Fork

This is a fork of the classic game **Rogue**, originally developed in the early 1980s. The purpose of this fork is to modernize the build process and address compatibility issues while maintaining the integrity of the original gameplay.

## Features of this Fork

- **Build Warnings and Errors Fixed**: 
  - Resolved deprecated and incompatible code issues.
  - Improved cross-platform compatibility with modern compilers.

- **Alternate Build Systems**:
  - Added support for **CMake** and **Meson** in addition to the original Automake.
  - Simplified build process for modern development environments.

- **Faithful to Original Gameplay**:
  - No gameplay changes or balancing modifications.
  - Focused exclusively on codebase and build improvements.

## License Information

This project is distributed under licenses consistent with the original **Rogue** source code. The original work is attributed to Michael Toy, Ken Arnold, and Glenn Wichman, with additional contributions and code portions under licenses from Nicholas J. Kisseberth and David Burren. 

- The game itself, including the main source code, is licensed under conditions that allow redistribution and modification with proper attribution and disclaimers.
- Specific files, such as `state.c`, `mdport.c`, and `xcrypt.c`, are derived from works by Nicholas J. Kisseberth and David Burren, respectively, and are distributed under compatible terms.

For full details, see the `LICENSE` file.

## Requirements

### General Requirements
- C compiler supporting C89 or later.
- Make or equivalent build tool.

### For CMake Build:
- CMake 3.15 or newer.

### For Meson Build:
- Meson 0.59 or newer.
- Ninja or compatible build backend.

## Building and Running

### Automake (Original Build System)
```sh
./configure
make
./rogue
```

### CMAKE
```sh
mkdir build && cd build
cmake ..
make
./rogue
```

### Meson
```sh
meson setup build
meson compile -C build
./build/rogue
```

## Contributing

Contributions are welcome to further improve code portability, enhance build systems, or fix issues. Please open a pull request or issue if you have suggestions or bug reports.

## Acknowledgments

Special thanks to the original creators of Rogue, Michael Toy, Ken Arnold, and Glenn Wichman, and to Nicholas J. Kisseberth and David Burren for their contributions to specific parts of the codebase. Their work laid the foundation for this timeless game.
