cmake_minimum_required(VERSION 3.17)
set(CMAKE_TOOLCHAIN_FILE $ENV{HOME}/vcpkg/scripts/buildsystems/vcpkg.cmake CACHE STRING "Vcpkg toolchain file")
project(URT VERSION 1.0 DESCRIPTION "URT")

# Compiler options
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_subdirectory(src)

target_include_directories(URT PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/include")

# Compiler and linker options
target_compile_options(URT PRIVATE -Wall -O3 -march=native)

find_package(OpenMP REQUIRED)
target_link_libraries(URT PRIVATE OpenMP::OpenMP_CXX)

#set(LAPACK_LIB "/usr/lib/x86_64-linux-gnu/lapack/liblapack.a")
#set(OPENBLAS_LIB "/usr/lib/x86_64-linux-gnu/libopenblas.a")

target_compile_definitions(URT PRIVATE USE_ARMA)
#find_package(Armadillo REQUIRED)
#target_link_libraries(URT PRIVATE ${ARMADILLO_LIBRARIES})
target_include_directories(URT PRIVATE /usr/local/mlpack/include)

#find_package(OpenBLAS REQUIRED)
#target_link_libraries(URT PRIVATE OpenBLAS::OpenBLAS)
target_compile_definitions(URT PUBLIC USE_BLAS)
