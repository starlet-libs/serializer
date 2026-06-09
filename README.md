# Starlet Serializer

![Tests](https://github.com/starlet-libs/serializer/actions/workflows/test.yml/badge.svg)
[![C++20](https://img.shields.io/badge/C%2B%2B-20-blue.svg)](https://isocpp.org/std/the-standard)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A lightweight serialization library for **Starlet** projects to handle both data reading and writing.

## Features

### File Format Support
- **Images**:
  - BMP (24-bit)
  - TGA (24/32-bit uncompressed)
- **Meshes**:
  - PLY (ASCII w/ positions, normals, colors, texture coordinates)
  - OBJ (positions, normals, texture coordinates, vertex colors, n-gon triangulation)
- **Scenes**: Custom text-based scene format with models, lights, cameras, textures, primitives

### Core Utilities
- **File I/O**: Binary and text file loading
- **Parsing Primitives**: 
  - Type-safe parsers: `parseBool`, `parseUInt`, `parseFloat`, `parseVec2f/3f/4f`
  - Token extraction with `parseToken`
  - Whitespace handling: `skipWhitespace`, `skipToNextLine`, `trimEOL`
  - Error-safe macros: `STARLET_PARSE_OR`, `STARLET_PARSE_STRING_OR`

## Dependencies
  - [starlet-math](https://github.com/starlet-libs/math) (auto-fetched)
  - [starlet-logger](https://github.com/starlet-libs/logger) (auto-fetched)

## Installation

### Prerequisites
- C++20 or later
- One of the following Build Systems,
    - CMake 3.20+
    - Meson 1.1+

### Using as a Dependency

#### CMake
```cmake
include(FetchContent)

FetchContent_Declare(starlet_serializer
  GIT_REPOSITORY https://github.com/starlet-libs/serializer.git
  GIT_TAG main
)
FetchContent_MakeAvailable(starlet_serializer)

target_link_libraries(app_name PRIVATE starlet_serializer)
```

#### Meson
> **Note:** Meson does not fetch dependencies automatically. Add the [`starlet_serializer.wrap`](./subprojects/starlet_serializer.wrap) file to your project's `subprojects` directory.

In your `meson.build`:

```python
starlet_serializer = subproject('starlet_serializer')
starlet_serializer_dep = starlet_serializer.get_variable('starlet_serializer_dep')
executable('app_name', 'main.cpp', dependencies: starlet_serializer_dep)
```

### Building and Testing
```bash
git clone https://github.com/starlet-libs/serializer.git
cd serializer
```

#### CMake
```bash
cmake -B build -DBUILD_TESTS=ON
cmake --build build
ctest --test-dir build
```

#### Meson
```bash
meson setup build -Dbuild_tests=true
meson compile -C build
meson test -C build
```

## License
MIT License - see [LICENSE](./LICENSE) for details.
