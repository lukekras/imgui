cmake_minimum_required(VERSION 3.21)
project(imgui)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED YES)
set(CMAKE_CXX_EXTENSIONS NO)

# Export IMGUI_SOURCE_DIR, IMGUI_SOURCES, IMGUI_BACKENDS_DIR, IMGUI_BACKEND_SOURCES,
# when imgui is an embedded project
set(IMGUI_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(IMGUI_BACKENDS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/backends)

add_subdirectory(examples/example_glfw_opengl3)
add_subdirectory(examples/example_glfw_metal)