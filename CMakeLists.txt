#cmake_minimum_required(VERSION 3.5)

#set(CMAKE_CXX_STANDARD 11)

#find_package(OpenGL REQUIRED)
#find_package(GLUT REQUIRED)



#include_directories(lib/glm/include lib/stb/include lib/assimp/include)
#include_directories(lib/glfw/include)
#include_directories( ${OPENGL_INCLUDE_DIRS}  ${GLUT_INCLUDE_DIRS}  )
#include_directories(lib/glad/include)

#add_executable(main src/common/main.cpp src/opengl.cpp src/common/utils.cpp src/common/mesh.cpp src/common/image.cpp src/common/application.cpp)


# Project definition
cmake_minimum_required(VERSION 3.5)
project(test_env_map)
set(CMAKE_CXX_STANDARD 11)

#find_package(ASSIMP 4.0 REQUIRED)
#if(ASSIMP_FOUND)
#    include_directories(${ASSIMP_INCLUDE_DIR})
#endif()

# Source files
set(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")
set(LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/lib")
set(SOURCES ${SRC_DIR}/common/main.cpp ${SRC_DIR}/common/utils.cpp ${SRC_DIR}/common/mesh.cpp ${SRC_DIR}/common/image.cpp ${SRC_DIR}/common/application.cpp ${SRC_DIR}/opengl.cpp)

# Executable definition and properties
add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE "${SRC_DIR}")
include_directories(${LIB_DIR}/glm/include ${LIB_DIR}/stb/include ${LIB_DIR}/assimp/include)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)

# GLFW
set(GLFW_DIR "${LIB_DIR}/glfw")
set(GLFW_BUILD_EXAMPLES OFF CACHE INTERNAL "Build the GLFW example programs")
set(GLFW_BUILD_TESTS OFF CACHE INTERNAL "Build the GLFW test programs")
set(GLFW_BUILD_DOCS OFF CACHE INTERNAL "Build the GLFW documentation")
set(GLFW_INSTALL OFF CACHE INTERNAL "Generate installation target")
add_subdirectory("${GLFW_DIR}")
target_link_libraries(${PROJECT_NAME} "glfw" "${GLFW_LIBRARIES}")
target_include_directories(${PROJECT_NAME} PRIVATE "${GLFW_DIR}/include")
target_compile_definitions(${PROJECT_NAME} PRIVATE "GLFW_INCLUDE_NONE")

# glad
set(GLAD_DIR "${LIB_DIR}/glad")
add_library("glad" "${GLAD_DIR}/src/glad.c")

target_include_directories("glad" PRIVATE "${GLAD_DIR}/include")
target_include_directories(${PROJECT_NAME} PRIVATE "${GLAD_DIR}/include")
target_link_libraries(${PROJECT_NAME} "glad" "${CMAKE_DL_LIBS}")

add_library(stb "${LIB_DIR}/stb/src/libstb.c")


target_link_libraries(${PROJECT_NAME}  /home/fei/Downloads/assimp/lib/libassimp.so)
target_link_libraries(${PROJECT_NAME}  stb)
