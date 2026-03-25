cmake_minimum_required(VERSION 3.30)
project(sticazzi_apps)

set(Sticazzi_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../libsticazzi/build")

add_subdirectory(app1)
add_subdirectory(app2)