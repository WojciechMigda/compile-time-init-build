cmake_minimum_required(VERSION 3.16)
project(compile_time_init_build)


add_executable(compilation_benchmark
    big_nexus.cpp
)

if (CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    target_compile_options(compilation_benchmark
        PRIVATE
            -ferror-limit=8
            -ftime-report
            -ftime-trace
    )

elseif (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_compile_options(compilation_benchmark
        PRIVATE
            -fmax-errors=8
            -ftime-report
    )
endif()


target_compile_options(compilation_benchmark
    PRIVATE
        -ftemplate-backtrace-limit=0
)

target_link_libraries(compilation_benchmark PRIVATE cib)
