# Jakt NES Monster

Creating a NES emulator in the [jakt](https://github.com/SerenityOS/jakt) programming language.

Make sure you have libsdl2+SDL2 headers installed, and build and install the jakt compiler into your PATH.

Then, you can build using (Linux):

```
> jakt src/main.jakt -l SDL2 -I <path to Jakt runtime directory> -O -o jakt_nes
```

On macOS, you can use (be sure to update versions to match your SDL2 version):

```
> jakt src/main.jakt -l SDL2 -I /opt/homebrew/Cellar/sdl2/2.0.22/include -L /opt/homebrew/Cellar/sdl2/2.0.22/lib -I ../jakt/runtime -O -o jakt_nes
```
