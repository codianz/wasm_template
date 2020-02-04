project (client)
cmake_minimum_required(VERSION 3.5.1)

add_definitions(-std=c++11 -O3)
include_directories(include)

file(GLOB SOURCES src/*.cpp)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/public")
add_executable(main ${SOURCES})

set(CMAKE_C_FLAGS "-s USE_SDL=2")
set(CMAKE_CXX_FLAGS "-s USE_SDL=2")
set(CMAKE_EXECUTABLE_SUFFIX ".wasm.js")

set_target_properties(main PROPERTIES LINK_FLAGS "-s WASM=1 -s BINARYEN_METHOD='native-wasm' -s EXPORTED_FUNCTIONS='[_main]'")
