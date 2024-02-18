cmake_minimum_required(VERSION 3.17)
set(CMAKE_TOOLCHAIN_FILE $ENV{HOME}/vcpkg/scripts/buildsystems/vcpkg.cmake CACHE STRING "Vcpkg toolchain file")
project(URT VERSION 1.0 DESCRIPTION "URT")

# Compiler options
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_subdirectory(src)

target_include_directories(URT PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/include")

# Compiler and linker options
target_compile_options(URT PRIVATE -Wall -O3 -march=native)

find_package(OpenMP REQUIRED)
target_link_libraries(URT PRIVATE OpenMP::OpenMP_CXX)

target_compile_definitions(URT PRIVATE USE_ARMA)
find_package(Armadillo REQUIRED)
target_link_libraries(URT PRIVATE ${ARMADILLO_LIBRARIES})
target_include_directories(URT PRIVATE ${ARMADILLO_INCLUDE_DIRS})

find_package(OpenBLAS REQUIRED)
target_link_libraries(URT PRIVATE OpenBLAS::OpenBLAS)
target_compile_definitions(URT PUBLIC USE_BLAS)
