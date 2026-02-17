# godot-cpp-template
This repository serves as a quickstart template for GDExtension development with Godot 4.5+.

## Information
This is a template for using the prebuilt Godot C++ bindings. This template is based on the 4.5 stable release of [godot-cpp](https://github.com/godotengine/godot-cpp) and does not include the source project as submodule, but instead relies on the prebuilt bindings available for your system.

If you are using MSYS2 you can install the prebuilt bindings using the following command for the x86_64 architecture:

```bash
pacman -S mingw-w64-x86_64-godot-cpp
```

For other MSYS2 architectures, you can replace `x86_64` with the appropriate architecture (e.g., `i686` for 32-bit).

## Requirements
- MSYS2 (for Windows)
- CMake
- Godot C++ bindings (prebuilt)
- C++ compiler (e.g., g++)
- Python (for SCons)
- SCons (build system)
- Godot Engine (version 4.5 or later)

The CMakeLists.txt file is configured to find the prebuilt Godot C++ bindings for MSYS2 and link against them. You may need to adjust the paths in the CMakeLists.txt file to point to the correct location of the prebuilt bindings on your system.

## Note
If you want to target an early versions of Godot 4, you may want to download and replace the files in gdextension and tools folders from the Godot C++ repository.
