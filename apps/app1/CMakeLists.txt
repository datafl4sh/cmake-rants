cmake_minimum_required(VERSION 3.30)
project(app1)

find_package(Sticazzi REQUIRED)

add_executable(app1 app1.cpp)
target_link_libraries(app1 sticazzi::sticazzi)