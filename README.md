# My Minimal ImGui Project

This project consits in creating a instant mode gui in C++ using **Dear ImGui** and **ImPlot** with **SDL2** and **OpenGL3** backend.

For now, the main file consited in displaying the demo proposed by the creator, build using cmake.

To create your own GUI, see in the main files the `ImGui:ShowDemoWindow()` and `ImPlot:ShowDemoWindow()` functions calls and the window created right after. Replace those calls with the call of a functions where you define windows. (Don't forget to modify CMakeLists.txt file if needed). You can find the examples provided of those two functions in the `examples` folder. These piece of code are a copy of demo from the Dear ImGui and ImPlot repo, but not builds, the build ones are those pulled during fetching of repos.

## Sources
[Dear ImGui](https://github.com/ocornut/imgui)

[ImPlot](https://github.com/epezent/implot/)

## Build
### Dependancies
`Dear ImGui` and `ImPlot` are fetched and build during the compile process

Requier SDL2 and OpenGL3

```bash
sudo apt install libsdl2-dev # for SDL2
```

Alternatively if you want to build SDL2 inside the project, add those lines in the CMakeLists.txt

```cmake
FetchContent_Declare(
  SDL2
  GIT_REPOSITORY "https://github.com/libsdl-org/SDL.git"
  GIT_TAG release-2.0.22
)

FetchContent_MakeAvailable(SDL2)
```

### build
Inside the parent folder
```bash
mkdir -p build && cd build
cmake ..
cmake --build .
```

### Launch executable
```bash
./minimal_gui
```
