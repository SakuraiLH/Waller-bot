cmake_minimum_required (VERSION 3.1)
project(waller)
set(CMAKE_CXX_STANDARD 17)

set(MIRAI_CPP_BUILD_EXAMPLES OFF CACHE BOOL "Build examples" FORCE)
add_subdirectory(mirai-cpp)

if(MSVC)
    add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
    add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")
    message(STATUS "optional: /UTF-8")   
endif(MSVC)

add_executable(${PROJECT_NAME} src/main.cpp)
include_directories(include)
target_link_libraries(${PROJECT_NAME} PRIVATE mirai-cpp)
target_compile_definitions(${PROJECT_NAME} PRIVATE MIRAICPP_STATICLIB)

if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_link_libraries(${PROJECT_NAME} PRIVATE pthread)
    target_link_libraries(${PROJECT_NAME} PRIVATE -static-libgcc -static-libstdc++)
endif()
