cmake_minimum_required(VERSION 3.17)
project(URT VERSION 1.0 DESCRIPTION "URT with OpenBLAS support")

# Set the C++ standard
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED True)


# Add the URT library target
add_subdirectory(src)
add_subdirectory(include)

# Compiler options
target_compile_options(URT PRIVATE -march=native)

find_package(OpenMP REQUIRED)
target_link_libraries(URT PRIVATE OpenMP::OpenMP_CXX)

find_package(Armadillo REQUIRED)
target_link_libraries(URT PRIVATE ${ARMADILLO_LIBRARIES})
target_include_directories(URT PRIVATE ${ARMADILLO_INCLUDE_DIRS})
target_compile_definitions(URT PUBLIC USE_ARMA)

find_package(OpenBLAS REQUIRED)
target_link_libraries(URT PRIVATE OpenBLAS::OpenBLAS)
target_compile_definitions(URT PUBLIC USE_BLAS)
