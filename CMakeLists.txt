cmake_minimum_required(VERSION 3.16)

# Project configuration
project(vk-tutorial)

add_executable(vk-tutorial src/main.cxx)

# C++ compiler requirements
set(gcc_like_cxx "$<COMPILE_LANG_AND_ID:CXX,ARMClang,AppleClang,Clang,GNU,LCC>")
set(msvc_cxx "$<COMPILE_LANG_AND_ID:CXX,MSVC>")
add_library(compiler_flags INTERFACE)
target_compile_features(compiler_flags INTERFACE cxx_std_17)
target_compile_options(compiler_flags INTERFACE
        "$<${gcc_like_cxx}:$<BUILD_INTERFACE:-Wall;-Wextra;-Wall;-O2>>"
        "$<${msvc_cxx}:$<BUILD_INTERFACE:-W4>>")

target_link_libraries(vk-tutorial PRIVATE glfw vulkan dl pthread X11 Xxf86vm Xrandr Xi)
