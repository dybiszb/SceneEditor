cmake_minimum_required(VERSION 3.6)
project(SceneEditor)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -lmingw32")
set(CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${SceneEditor_SOURCE_DIR}/cmake-modules")


find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIR})

set(SOURCE_FILES main.cpp main.cpp)
add_executable(SceneEditor ${SOURCE_FILES})
target_link_libraries(SceneEditor ${SDL2_LIBRARY})

# ==============================================================================
# Copy .dll if on Windows
# ==============================================================================
if(WIN32)
    add_custom_command(TARGET SceneEditor POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy_if_different
            "${SDL2_INCLUDE_DIR}/../../bin/SDL2.dll"
            $<TARGET_FILE_DIR:SceneEditor>)
endif(WIN32)