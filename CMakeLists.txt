cmake_minimum_required(VERSION 3.3)
project(glez C)

find_package(Freetype REQUIRED)
find_package(GLEW REQUIRED)
find_package(OpenGL REQUIRED)
find_package(PNG REQUIRED)

if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -fPIC")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g3 -ggdb")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3")

file(GLOB SOURCES "src/*.c")
file(GLOB SOURCES "ftgl/*.c")

add_library(glez32 SHARED ${SOURCES})
add_library(glez64 SHARED ${SOURCES})

include_directories(include)
include_directories(SYSTEM ftgl ${FREETYPE_INCLUDE_DIRS} ${GLEW_INCLUDE_DIRS} ${OPENGL_INCLUDE_DIRS} ${PNG_INCLUDE_DIRS})

list(APPEND GLEZ_LIBRARIES m rt freetype GLEW GL png)

target_link_libraries(glez32 ${GLEZ_LIBRARIES})
target_link_libraries(glez64 ${GLEZ_LIBRARIES})

set_target_properties(glez32 PROPERTIES 
    PUBLIC_HEADER include/glez.h
    LIBRARY_OUTPUT_DIRECTORY "bin32"
    OUTPUT_NAME "glez"
    COMPILE_FLAGS "-m32"
    LINK_FLAGS "-m32")
    
set_target_properties(glez64 PROPERTIES 
    PUBLIC_HEADER include/glez.h
    LIBRARY_OUTPUT_DIRECTORY "bin64"
    OUTPUT_NAME "glez")