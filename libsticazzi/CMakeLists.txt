cmake_minimum_required(VERSION 3.20)
project(libsticazzi)

find_package(Eigen3 REQUIRED)

add_subdirectory(contrib/sol2)

add_library(sticazzi SHARED src/sticazzi.cpp)
target_link_libraries(sticazzi
    #sol2::sol2
    Eigen3::Eigen
)

target_include_directories(sticazzi PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

install(TARGETS sticazzi
    EXPORT SticazziTargets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)

install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/cmake/"
        DESTINATION lib/cmake/sticazzi)

install(DIRECTORY include/ DESTINATION include)

install(EXPORT SticazziTargets
    FILE SticazziTargets.cmake
    NAMESPACE sticazzi::
    DESTINATION lib/cmake/sticazzi
)

export(TARGETS sticazzi
       NAMESPACE sticazzi::
       FILE "${CMAKE_CURRENT_BINARY_DIR}/SticazziTargets.cmake")

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/SticazziConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/SticazziConfigVersion.cmake"
    DESTINATION lib/cmake/sticazzi
)

include(CMakePackageConfigHelpers)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/SticazziConfigVersion.cmake"
    VERSION 0.0.0
    COMPATIBILITY SameMajorVersion
)

configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/SticazziConfig.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/SticazziConfig.cmake"
    INSTALL_DESTINATION lib/cmake/sticazzi
)
