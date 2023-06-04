cmake_minimum_required(VERSION 3.24.2)

cmake_policy(SET CMP0135 NEW)

project(fuzz_project)

set(CMAKE_CXX_STANDARD 20)

include(FetchContent)
FetchContent_Declare(fuzztest URL https://github.com/google/fuzztest/archive/refs/heads/main.zip)

# Prevent fuzztest from unsetting our policies
function(cmake_minimum_required)
endfunction()
FetchContent_MakeAvailable(fuzztest)

enable_testing()

include(GoogleTest)

fuzztest_setup_fuzzing_flags()
add_executable(fuzz_test fuzz_test.cpp)

link_fuzztest(fuzz_test)
gtest_discover_tests(fuzz_test)
