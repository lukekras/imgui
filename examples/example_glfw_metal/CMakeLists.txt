project(example_glfw_metal)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fobjc-weak")

cmake_path(GET CMAKE_CURRENT_SOURCE_DIR PARENT_PATH IMGUI_EXAMPLES_DIR)
set(IMGUI_3RDPARTY_DEPENDENCY_DIR ${IMGUI_EXAMPLES_DIR}/libs)

cmake_path(GET IMGUI_EXAMPLES_DIR PARENT_PATH IMGUI_SOURCE_DIR)
include_directories(${IMGUI_SOURCE_DIR})

set(IMGUI_BACKENDS_DIR ${IMGUI_SOURCE_DIR}/backends)
include_directories(${IMGUI_BACKENDS_DIR})

set(IMGUI_BACKEND_SOURCES)
list(APPEND IMGUI_BACKEND_SOURCES ${IMGUI_BACKENDS_DIR}/imgui_impl_metal.mm)
list(APPEND IMGUI_BACKEND_SOURCES ${IMGUI_BACKENDS_DIR}/imgui_impl_glfw.cpp)

set(IMGUI_SOURCES)
list(APPEND IMGUI_SOURCES ${IMGUI_SOURCE_DIR}/imgui.cpp)
list(APPEND IMGUI_SOURCES ${IMGUI_SOURCE_DIR}/imgui_draw.cpp)
list(APPEND IMGUI_SOURCES ${IMGUI_SOURCE_DIR}/imgui_widgets.cpp)
list(APPEND IMGUI_SOURCES ${IMGUI_SOURCE_DIR}/imgui_tables.cpp)
list(APPEND IMGUI_SOURCES ${IMGUI_SOURCE_DIR}/imgui_demo.cpp)

set(app_name example_glfw_metal)
add_executable(${app_name} main.mm ${IMGUI_SOURCES} ${IMGUI_BACKEND_SOURCES})

find_package(glfw3 3.3 REQUIRED)
target_link_libraries(${app_name} glfw)

set(IMGUI_FRAMEWORK_DEPS)
list(APPEND IMGUI_FRAMEWORK_DEPS "-framework Metal")
list(APPEND IMGUI_FRAMEWORK_DEPS "-framework MetalKit")
list(APPEND IMGUI_FRAMEWORK_DEPS "-framework Cocoa")
#list(APPEND IMGUI_FRAMEWORK_DEPS "-framework IOKit")
#list(APPEND IMGUI_FRAMEWORK_DEPS "-framework CoreVideo")
list(APPEND IMGUI_FRAMEWORK_DEPS "-framework QuartzCore")
target_link_libraries(${app_name} ${IMGUI_FRAMEWORK_DEPS})