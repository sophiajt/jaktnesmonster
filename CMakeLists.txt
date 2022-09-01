cmake_minimum_required(VERSION 3.16)

project(
    jaktnesmonster
    DESCRIPTION "NES Emulator written in Jakt"
    HOMEPAGE_URL "https://github.com/jntrnr/jaktnesmonster"
    LANGUAGES CXX)

find_package(Jakt CONFIG REQUIRED)
find_package(SDL2 CONFIG REQUIRED)

add_jakt_executable(jakt_nes
    MAIN_SOURCE src/main.jakt
    MODULE_SOURCES
        src/apu.jakt
        src/cart.jakt
        src/cpu.jakt
        src/ppu.jakt
        src/sdl.jakt
        src/system.jakt
        src/video.jakt
)

target_compile_definitions(jakt_nes PRIVATE SDL_MAIN_HANDLED)
target_link_libraries(jakt_nes PRIVATE SDL2::SDL2)
