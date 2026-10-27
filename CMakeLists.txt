cmake_minimum_required(VERSION 3.20)
project(minix_203 C)

set(CMAKE_C_STANDARD 90)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

add_compile_options(
        -nostdinc
        -m32
        -Wall
        -Wextra
        -pedantic-errors
        -Werror=newline-eof
        -Werror=declaration-after-statement
        -Werror=comment
)

add_compile_definitions(
        _MINIX=1
        _POSIX_SOURCE=1
        _SYSTEM=1
        _ANSI=31459
        CHIP=1          # 1 = INTEL <minix/config.h>
        _WORD_SIZE=4    # 32-bit MINIX
)

include_directories(
        BEFORE SYSTEM
        ${CMAKE_SOURCE_DIR}/usr/include
)

include_directories(
        ${CMAKE_SOURCE_DIR}/usr/src
        ${CMAKE_SOURCE_DIR}/usr/src/kernel
        ${CMAKE_SOURCE_DIR}/usr/src/mm
        ${CMAKE_SOURCE_DIR}/usr/src/fs
)

file(GLOB_RECURSE MINIX_SOURCES
        "${CMAKE_SOURCE_DIR}/usr/src/kernel/*.c"
        "${CMAKE_SOURCE_DIR}/usr/src/kernel/*.h"
        "${CMAKE_SOURCE_DIR}/usr/src/mm/*.c"
        "${CMAKE_SOURCE_DIR}/usr/src/mm/*.h"
        "${CMAKE_SOURCE_DIR}/usr/src/fs/*.c"
        "${CMAKE_SOURCE_DIR}/usr/src/fs/*.h"
        "${CMAKE_SOURCE_DIR}/usr/src/lib/*.c"
        "${CMAKE_SOURCE_DIR}/usr/src/servers/*.c"
)

add_executable(minix_index EXCLUDE_FROM_ALL ${MINIX_SOURCES})