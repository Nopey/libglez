#find . -iname \*.c
set (SOURCE_FILES
./src/glez.c
./src/program.c
./src/fonts.c
./src/textures.c
./src/draw.c
./ftgl/text-buffer.c
./ftgl/texture-atlas.c
./ftgl/vertex-attribute.c
./ftgl/makefont.c
./ftgl/vertex-buffer.c
./ftgl/distance-field.c
./ftgl/mat4.c
./ftgl/vector.c
./ftgl/texture-font.c
./ftgl/font-manager.c
./ftgl/edtaa3func.c
./ftgl/platform.c
./ftgl/utf8-utils.c)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(SYSTEM ${CMAKE_CURRENT_SOURCE_DIR}/ftgl)

#init empty list
set(LINK_LIBRARIES )


find_package(OpenGL)
list(APPEND LINK_LIBRARIES ${OPENGL_gl_LIBRARY})
include_directories(SYSTEM ${OPENGL_INCLUDE_DIR})
find_package(GLEW)
list(APPEND LINK_LIBRARIES ${GLEW_LIBRARIES})
include_directories(SYSTEM ${GLEW_INCLUDE_DIRS})
find_package(Freetype)
list(APPEND LINK_LIBRARIES ${FREETYPE_LIBRARIES})
include_directories(SYSTEM ${FREETYPE_INCLUDE_DIRS})

add_compile_options(-m32)

add_library(glez STATIC ${SOURCE_FILES})
target_link_libraries(glez ${LINK_LIBRARIES})