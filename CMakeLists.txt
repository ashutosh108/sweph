cmake_minimum_required(VERSION 3.12)
project(sweph LANGUAGES C)

add_library(swedll32 SHARED 
    src/swecl.c
    src/swedate.c
    src/swedllst.c
    src/swehel.c
    src/swehouse.c
    src/swejpl.c
    src/swemmoon.c
    src/swemplan.c
    src/sweph.c
    src/swephlib.c)
target_compile_definitions(swedll32 PRIVATE MAKE_DLL)
if ( MSVC )
    # W4996 is "strncpy may be unsafe, use strncpy_s", etc.
    # But we don't want to change the way sweph is using those functions already.
    target_compile_options(swedll32 PRIVATE "/wd4996")
endif()

if ( WIN32 )
    # gcc on windows insists on producing "libswedll32.dll" by default,
    # but we want "swedll32.dll" instead
    set(CMAKE_SHARED_LIBRARY_PREFIX_C "")
endif()
