include_directories(${IMGUI_SOURCE_DIR})
include_directories(${IMGUI_BACKENDS_DIR})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fobjc-weak")

if (NOT DEFINED IMGUI_BACKEND_SOURCES)
    set(IMGUI_BACKEND_SOURCES)
endif ()
list(APPEND IMGUI_BACKEND_SOURCES ${IMGUI_BACKENDS_DIR}/imgui_impl_metal.mm)
list(APPEND IMGUI_BACKEND_SOURCES ${IMGUI_BACKENDS_DIR}/imgui_impl_glfw.cpp)

if (NOT DEFINED IMGUI_SOURCES)
    set(IMGUI_SOURCES)
endif ()
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