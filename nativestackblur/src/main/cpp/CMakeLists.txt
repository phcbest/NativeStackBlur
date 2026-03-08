cmake_minimum_required(VERSION 3.10.2)

project(blur C)

add_library(blur SHARED blur.c)

find_library(log-lib log)
find_library(jnigraphics-lib jnigraphics)

# Make the ELF loadable on both 4KB and 16KB page-size devices.
set_target_properties(
    blur
    PROPERTIES LINK_FLAGS "-Wl,-z,max-page-size=16384"
)

target_link_libraries(
    blur
    ${log-lib}
    ${jnigraphics-lib}
)
