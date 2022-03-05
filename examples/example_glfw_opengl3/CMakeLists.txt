include_directories(${IMGUI_SOURCE_DIR})
include_directories(${IMGUI_BACKENDS_DIR})

set(IMGUI_BACKEND_SOURCES
    ${IMGUI_BACKENDS_DIR}/imgui_impl_opengl3.cpp
    ${IMGUI_BACKENDS_DIR}/imgui_impl_glfw.cpp
)

set(IMGUI_SOURCES
    ${IMGUI_SOURCE_DIR}/imgui.cpp
    ${IMGUI_SOURCE_DIR}/imgui_draw.cpp
    ${IMGUI_SOURCE_DIR}/imgui_widgets.cpp
    ${IMGUI_SOURCE_DIR}/imgui_tables.cpp
    ${IMGUI_SOURCE_DIR}/imgui_demo.cpp
)

add_executable(example_glfw_opengl3 main.cpp ${IMGUI_SOURCES} ${IMGUI_BACKEND_SOURCES})

find_package(glfw3 3.3 REQUIRED)
target_link_libraries(example_glfw_opengl3 glfw)

find_package(OpenGL REQUIRED)
target_link_libraries(example_glfw_opengl3 OpenGL::GL)

find_library(METAL Metal)
if (NOT METAL)
    message(FATAL_ERROR "Metal not found")
endif()

target_link_libraries(example_glfw_opengl3 ${METAL})