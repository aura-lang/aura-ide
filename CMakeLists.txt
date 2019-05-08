cmake_minimum_required(VERSION 3.8)

project("aura-ide")

add_subdirectory("deps")

# Compile the IDE.
file(GLOB_RECURSE AURA_IDE_FILES src/*.cpp src/*.hpp src/*.h src/*.c)
add_executable(aura-ide ${AURA_IDE_FILES})
target_link_libraries(aura-ide imgui glad)