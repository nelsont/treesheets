# Sample build with makefile generator
#
#     cd <into-treesheets-source>
#     cmake -H. -Bb -DCMAKE_BUILD_TYPE=Release \
#         -DCMAKE_INSTALL_PREFIX=$PWD/i \
#         -DCMAKE_PROGRAM_PATH=<path-to-wx-config> # not always needed
#     cmake --build b --target install
#
# Sample build with IDE generator, like Xcode
#
#     cd <into-treesheets-source>
#     cmake -H. -Bb -GXcode \
#         -DCMAKE_INSTALL_PREFIX=$PWD/i \
#         -DCMAKE_PROGRAM_PATH=<path-to-wx-config> # not always needed
#     cmake --build b --config Release --target install
#
# Run program:
#
#     ./i/treesheets
#
# Should work on Windows, too. About helping FindwxWidgets to find wxWidgets
# consult: https://cmake.org/cmake/help/latest/module/FindwxWidgets.html

cmake_minimum_required(VERSION 3.1)
# CMAKE_CXX_STANDARD needs v3.1, could be lowered with minor effort

project(treesheets)

set(CMAKE_CXX_STANDARD 11)

find_package(wxWidgets REQUIRED aui adv core xml net)
include(${wxWidgets_USE_FILE})

file(GLOB sources src/*.cpp src/*.h)
add_executable(treesheets ${sources})

target_link_libraries(treesheets PRIVATE ${wxWidgets_LIBRARIES})

install(TARGETS treesheets DESTINATION .)
install(DIRECTORY TS/ DESTINATION .)
