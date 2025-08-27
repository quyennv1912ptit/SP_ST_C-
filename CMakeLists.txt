cmake_minimum_required(VERSION 3.10)
project(SP_ST)

set(CMAKE_CXX_STANDARD 17)

if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mwindows")
endif()

include_directories(${CMAKE_SOURCE_DIR}/include)
link_directories(${CMAKE_SOURCE_DIR}/lib)

add_executable(SP_ST src/main.cpp)

target_link_libraries(SP_ST sfml-graphics sfml-window sfml-system sfml-audio)

add_custom_command(TARGET SP_ST POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "${CMAKE_SOURCE_DIR}/lib/sfml-graphics-3.dll"
    "${CMAKE_SOURCE_DIR}/lib/sfml-window-3.dll"
    "${CMAKE_SOURCE_DIR}/lib/sfml-system-3.dll"
    "${CMAKE_SOURCE_DIR}/lib/sfml-audio-3.dll"
    $<TARGET_FILE_DIR:SP_ST>
)