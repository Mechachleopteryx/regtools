cmake_minimum_required(VERSION 2.8)

set(TEST_LIBS variants)
set(TEST_SOURCES
    "test_variants_annotator.cc")

set(test_name TestVariants)
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D__STDC_LIMIT_MACROS")
include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})
include_directories("${PROJECT_SOURCE_DIR}/src/variants/")
include_directories("${PROJECT_SOURCE_DIR}/src/gtf/"
                    "${PROJECT_SOURCE_DIR}/src/utils/"
                    "${PROJECT_SOURCE_DIR}/src/junctions/"
                    "${PROJECT_SOURCE_DIR}/src/utils/bedtools/bedFile/"
                    "${PROJECT_SOURCE_DIR}/src/utils/bedtools/lineFileUtilities/"
                    "${PROJECT_SOURCE_DIR}/src/utils/bedtools/gzstream/"
                    "${PROJECT_SOURCE_DIR}/src/utils/bedtools/fileType/"
                    "${PROJECT_SOURCE_DIR}/src/utils/bedtools/stringUtilities/"
                    "${PROJECT_SOURCE_DIR}/src/utils/htslib/")
add_executable(${test_name} ${TEST_SOURCES})
target_link_libraries(${test_name} gtest gtest_main junctions bedtools gtf htslib)
set(NOSTRING_FLAG "-Wno-write-strings")
set_target_properties(${test_name} PROPERTIES COMPILE_FLAGS
    ${NOSTRING_FLAG})

add_test(${test_name} ${test_name})
