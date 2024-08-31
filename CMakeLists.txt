cmake_minimum_required(VERSION 3.22)

project(
  minimal_gui
  DESCRIPTION "My minimal C++ imgui"
  LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenGL REQUIRED)
find_package(SDL2 REQUIRED)

include(FetchContent)

FetchContent_Declare(
  imgui
  GIT_REPOSITORY "https://github.com/ocornut/imgui.git"
  # docking-latest
  GIT_TAG 226e0d579d2632a81d95f60bb5d65c70e55feb90
)
FetchContent_MakeAvailable(imgui)

FetchContent_Declare(
  implot
  GIT_REPOSITORY "https://github.com/epezent/implot.git"
  GIT_TAG f156599faefe316f7dd20fe6c783bf87c8bb6fd9
)
FetchContent_MakeAvailable(implot)

add_library(imgui
  ${imgui_SOURCE_DIR}/imgui.cpp
  ${imgui_SOURCE_DIR}/imgui.h
  ${imgui_SOURCE_DIR}/imconfig.h
  ${imgui_SOURCE_DIR}/imgui_demo.cpp
  ${imgui_SOURCE_DIR}/imgui_draw.cpp
  ${imgui_SOURCE_DIR}/imgui_internal.h
  ${imgui_SOURCE_DIR}/imgui_tables.cpp
  ${imgui_SOURCE_DIR}/imgui_widgets.cpp
  ${imgui_SOURCE_DIR}/imstb_rectpack.h
  ${imgui_SOURCE_DIR}/imstb_textedit.h
  ${imgui_SOURCE_DIR}/imstb_truetype.h
  ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl2.cpp
  ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl2.h
  ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp
  ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.h
  ${implot_SOURCE_DIR}/implot.h 
  ${implot_SOURCE_DIR}/implot_internal.h
  ${implot_SOURCE_DIR}/implot.cpp
  ${implot_SOURCE_DIR}/implot_items.cpp
  ${implot_SOURCE_DIR}/implot_demo.cpp 
)

target_include_directories(imgui PUBLIC ${imgui_SOURCE_DIR})
target_link_libraries(imgui PUBLIC SDL2::SDL2)

# Define the main executable
add_executable(${PROJECT_NAME} src/main.cpp)

target_include_directories(${PROJECT_NAME} PRIVATE
    ${imgui_SOURCE_DIR}
    ${implot_SOURCE_DIR}
    ${imgui_SOURCE_DIR}/backends
)

# Link SDL2 and ImGui to your project
target_link_libraries(${PROJECT_NAME} PRIVATE SDL2::SDL2 OpenGL::GL imgui)
