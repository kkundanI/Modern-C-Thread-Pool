cmake_minimum_required(VERSION 3.10)
project(modern_thread_pool)

set(CMAKE_CXX_STANDARD 17)

include_directories(include)

add_executable(example examples/basic.cpp)

