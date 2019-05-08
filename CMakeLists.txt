cmake_minimum_required(VERSION 3.8)

project("aura-ide")

# Add GLFW for window handling
set(GLFW_BUILD_EXAMPLES OFF)
set(GLFW_BUILD_TESTS OFF)
set(GLFW_BUILD_DOCS OFF)
add_subdirectory("glfw")

# Create the opengl context.
file(GLOB_RECURSE GLAD_FILES glad/src/*.c glad/)
add_library(glad STATIC ${GLAD_FILES})
target_include_directories(glad glad/include/)

# Compile imgui for the GUI interface
set(IMGUI_FILES 
    imgui/imgui_demo.cpp
    imgui/imgui_draw.cpp
    imgui/imgui.cpp
    imgui/imgui_widgets.cpp
    imgui/misc/cpp/imgui_stdlib.cpp
    imgui/examples/imgui_impl_opengl3.cpp
    imgui/examples/imgui_impl_glfw.cpp
)

add_library(imgui STATIC ${IMGUI_FILES})
target_include_directories(imgui 
    imgui/
    imgui/examples/
    imgui/misc/cpp/
)

target_link_libraries(imgui glad)
target_compile_definitions(imgui IMGUI_IMPL_OPENGL_LOADER_GLAD)


# Compile the IDE.
file(GLOB_RECURSE AURA_IDE_FILES ide/*.cpp ide/*.hpp ide/*.h ide/*.c)
add_executable(aura-ide ${AURA_IDE_FILES})
target_link_libraries(aura-ide imgui glad)