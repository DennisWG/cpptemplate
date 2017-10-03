project(cpptemplate_test VERSION 0.1 LANGUAGES CXX)

add_executable(test_cpptemplate
    dummy.cpp
)

if (CMAKE_BUILD_TYPE STREQUAL "Coverage")
    include(CodeCoverage)
    set_target_properties(
            test_cpptemplate PROPERTIES
            COMPILE_FLAGS "-O0 -g -fprofile-arcs -ftest-coverage"
            LINK_FLAGS "-O0 -g -lgcov -fprofile-arcs -ftest-coverage"
    )

    SETUP_TARGET_FOR_COVERAGE(
        coverage
        test_cpptemplate
        coverage_report
    )
endif()

target_link_libraries(test_cpptemplate
    lib_cpptemplate
)

add_test(test_cpptemplate test_cpptemplate)

install(TARGETS test_cpptemplate
    RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR}
)

export(TARGETS lib_cpptemplate FILE cpptemplate_config.cmake)