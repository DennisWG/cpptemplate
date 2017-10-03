project(cpptemplate_lib VERSION 0.1 LANGUAGES CXX)

add_library(lib_cpptemplate
	dummy.cpp
)

target_include_directories(lib_cpptemplate
    PUBLIC
	    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
	    $<INSTALL_INTERFACE:../include>
)

target_compile_features(lib_cpptemplate
    PUBLIC cxx_std_17
)

target_link_libraries(lib_cpptemplate
    boost
)

install(TARGETS lib_cpptemplate EXPORT cpptemplate_config
    ARCHIVE  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR}
)
install(DIRECTORY ../include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(EXPORT cpptemplate_config DESTINATION share/MyLibrary/cmake)

export(TARGETS lib_cpptemplate FILE cpptemplate_config.cmake)