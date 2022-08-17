- Jakt NES Monster

Creating a NES emulator in the [jakt]() programming language.

Currently assuming building in linux. Make sure you have libsdl2+SDL2 headers installed, and build and install the jakt compiler into your PATH.

Then, you can build using:

```
> jakt src/main.jakt -l SDL2 -I <path to Jakt runtime directory> -o jakt_nes -O
```
