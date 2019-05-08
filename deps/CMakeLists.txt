cmake_minimum_required(VERSION 3.8)

# Add GLFW for window handling
option(GLFW_BUILD_EXAMPLES "" OFF)
option(GLFW_BUILD_TESTS "" OFF)
option(GLFW_BUILD_DOCS "" OFF)
add_subdirectory("glfw")

# Create the opengl context.
file(GLOB_RECURSE GLAD_FILES glad/src/*.c glad/)
add_library(glad STATIC ${GLAD_FILES})
target_include_directories(glad PUBLIC
 glad/include/
)

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
target_include_directories(imgui PUBLIC
    imgui/
    imgui/examples/
    imgui/misc/cpp/
)

target_link_libraries(imgui glad glfw)
target_compile_definitions(imgui PUBLIC
    IMGUI_IMPL_OPENGL_LOADER_GLAD
)
