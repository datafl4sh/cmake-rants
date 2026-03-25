cmake_minimum_required(VERSION 3.30)
project(app2)

find_package(Sticazzi REQUIRED)

add_executable(app2 app2.cpp)
target_link_libraries(app2 sticazzi::sticazzi)