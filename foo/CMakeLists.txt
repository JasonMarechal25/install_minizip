cmake_minimum_required(VERSION 3.12)
project(foo)

find_package(minizip-ng)
# Define the library target
add_library(foo
        Foo.cpp
)

# Specify include directories
target_include_directories(foo
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)
target_link_libraries(foo
    PRIVATE
        MINIZIP::minizip
)

# Install the library
install(TARGETS foo
        DESTINATION lib
)

# Install the header file
install(FILES Foo.h
        DESTINATION include
)