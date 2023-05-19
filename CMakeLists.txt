cmake_minimum_required(VERSION 3.17)

project(vcross)

set(CMAKE_CXX_STANDARD 20)

if(NOT TARGET Vulkan)
    find_package(Vulkan CONFIG REQUIRED)
endif()

if(NOT TARGET glm)
    find_package(glm CONFIG REQUIRED)
endif()

if(NOT TARGET freetype)
    find_package(freetype CONFIG REQUIRED)
endif()

file(GLOB_RECURSE SOURCES src/*.*)
add_library(${PROJECT_NAME} STATIC ${SOURCES})

target_include_directories(${PROJECT_NAME} PUBLIC include)
target_link_libraries(${PROJECT_NAME} PUBLIC glm::glm freetype)
target_link_libraries(${PROJECT_NAME} PRIVATE Vulkan)

add_subdirectory(test vcross_test)