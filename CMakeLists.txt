cmake_minimum_required(VERSION 3.16)

project(cpp_temp VERSION 1.0 LANGUAGES CXX)
add_executable(cpp_temp main.cpp)

set_target_properties(cpp_temp PROPERTIES
        CXX_STANDARD 20
        CXX_STANDARD_REQUIRED ON
        CXX_EXTENSIONS OFF
        INTERPROCEDURAL_OPTIMIZATION TRUE
)

target_compile_options(cpp_temp PRIVATE
        $<$<CONFIG:DEBUG>: -Wall -Wextra -pedantic>
        $<$<CONFIG:Release>: -DNDEBUG -O2 -funroll-loops -ftree-vectorize>
)

target_compile_options(cpp_temp PRIVATE $<$<CXX_COMPILER_ID:GNU>:
        $<$<CONFIG:DEBUG>: -ggdb -Wformat=2 -Wconversion -Wlogical-op -Wshift-overflow=2 -Wduplicated-cond -Wcast-qual -Wcast-align>>
)

target_compile_options(cpp_temp PRIVATE $<$<CXX_COMPILER_ID:Clang>:
        $<$<CONFIG:DEBUG>:-Weverything -Wno-c++98-compat-pedantic -Wno-missing-prototypes>>
)
