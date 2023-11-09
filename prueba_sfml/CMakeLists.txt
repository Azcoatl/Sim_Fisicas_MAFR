cmake_minimum_required(VERSION 3.26)
project(prueba_sfml)

include(FetchContent)
set(BUILD_SHARED_LIBS OFF)
FETCHCONTENT_DECLARE(SFML GIT_REPOSITORY https://github.com/SFML/SFML.git GIT_TAG 2.5.1)
FETCHCONTENT_MAKEAVAILABLE(SFML)

set(CMAKE_CXX_STANDARD 17)

add_executable(prueba_sfml main.cpp)

find_package(box2d CONFIG REQUIRED)

target_link_libraries(prueba_sfml PRIVATE box2d::box2d sfml-system sfml-window sfml-graphics sfml-audio)
