# Jakt NES Monster

Creating a NES emulator in the [jakt](https://github.com/SerenityOS/jakt) programming language.

# Building

Make sure you have libsdl2+SDL2 headers installed, and build and install the jakt compiler into your PATH.

## Building using jakt directly

With jakt in your path and the install location of SDL2 known, you can build like so for Linux:

```
> jakt src/main.jakt -l SDL2 -I <path to Jakt runtime directory> -O -o jakt_nes
```

On macOS, you can use (be sure to update versions to match your SDL2 version):

```
> jakt src/main.jakt -l SDL2 -I /opt/homebrew/Cellar/sdl2/2.0.22/include -L /opt/homebrew/Cellar/sdl2/2.0.22/lib -I ../jakt/runtime -O -o jakt_nes
```

For Windows, keep reading into the CMake steps :^).

## Building using CMake

Instead of installing jakt into somewhere that's in your path, make sure to install jakt via the CMake build by setting CMAKE_INSTALL_PREFIX somewhere interesting, or passing --prefix on the command line . One decent option for prefix is "jakt-install".

```
jakt> cmake -B build -GNinja -DCMAKE_INSTALL_PREFIX=jakt-install -DCMAKE_CXX_COMPILER=clang++
jakt> cmake --build build
jakt> cmake --install build
# alternative to setting CMAKE_INSTALL_PREFIX
jakt> cmake --install build --prefix jakt-test
```

After that, you can build jaktnesmonster by passing the location of jakt CMake files to CMake. CMake should find SDL2 automatically, if it's in a standard install location for your platform (Linux, macOS, other Unix).

```
> cmake -G Ninja -B build -DCMAKE_PREFIX_PATH=../jakt/jakt-install -DCMAKE_CXX_COMPILER=clang++
> cmake --build build
# Alternatively
> ninja -C build
```

### Building on Windows

The easiest way to hook up SDL2 to CMake on windows is via [vcpkg](https://vcpkg.io/en/getting-started.html)

Ensure that you have the VS 2019 or 2022 toolset installed, including clang. MSVC is not supported.

Perform the above jakt install steps from a VS Developer Powershell instance.

Next, install SDL2 via vcpkg from a VS Developer PowerShell instance:

```powershell
git clone https://github.com/Microsoft/vcpkg.git
cd vcpkg
.\bootstrap-vcpkg.bat
.\vcpkg install sdl2:x64-windows
```

Finally, configure jaktnesmonster with CMake, passing your Windows install of jakt, the vcpkg toolchain file, and clang++ as the C++ compiler:

```powershell
cmake -B build -GNinja `
    -DCMAKE_PREFIX_PATH="..\jakt\jakt-install\share" `
    -DCMAKE_TOOLCHAIN_FILE="..\vcpkg\scripts\buildsystems\vcpkg.cmake" `
    -DCMAKE_CXX_COMPILER=clang++
```

Now you can build jakt_nes.exe via

```
> cmake --build build
```
or
```
> ninja -C build
```

Alternatively, using Visual Studio directly to build, you can create a CMakeSettings.json similar to:

```json
{
  "configurations": [
    {
      "name": "x64-Debug",
      "generator": "Ninja",
      "configurationType": "Debug",
      "inheritEnvironments": [ "clang_cl_x64_x64" ],
      "buildRoot": "${projectDir}\\out\\build\\${name}",
      "installRoot": "${projectDir}\\out\\install\\${name}",
      "cmakeCommandArgs": "-DCMAKE_PREFIX_PATH=\"..\\jakt\\jakt-install\\share\" ",
      "buildCommandArgs": "",
      "ctestCommandArgs": "",
      "cmakeToolchain": "..\\vcpkg\\scripts\\buildsystems\\vcpkg.cmake"
    }
  ]
}
```
