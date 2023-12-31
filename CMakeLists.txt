cmake_minimum_required(VERSION 3.15)
project(install_minizip VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 17)
include(FetchContent)

FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG        b10fad38c4026a29ea6561ab15fc4818170d1c10 # release-1.10.0
        OVERRIDE_FIND_PACKAGE
)
FetchContent_MakeAvailable(googletest)
find_package(googletest REQUIRED)




find_package(minizip)

if(NOT minizip_FOUND OR BUILD_MINIZIP)
    # Repository + tag
    set(MZ_REPOSITORY "https://github.com/zlib-ng/minizip-ng.git")
    set(MZ_TAG "4.0.3")
    # CMake flags
    set(MZ_LZMA "OFF" CACHE INTERNAL "")
    set(MZ_ZSTD "OFF" CACHE INTERNAL "")
    set(MZ_BZIP2 "OFF" CACHE INTERNAL "")
    set(MZ_PKCRYPT "OFF" CACHE INTERNAL "")
    set(MZ_WZAES "OFF" CACHE INTERNAL "")
    set(MZ_OPENSSL "OFF" CACHE INTERNAL "")
    set(MZ_ICONV "OFF" CACHE INTERNAL "")

    FetchContent_Declare(minizip
            GIT_REPOSITORY https://github.com/zlib-ng/minizip-ng.git
            GIT_TAG "4.0.1"
            OVERRIDE_FIND_PACKAGE
    )

    FetchContent_MakeAvailable(minizip)
endif()
find_package(minizip REQUIRED)

add_executable(install_minizip main.cpp)
add_subdirectory(foo)
add_subdirectory(packaging)