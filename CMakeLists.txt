#当文件全部放入到同一个文件夹下的cmakelists

# cmake_minimum_required(VERSION 3.31.0)
# project(planning)
# set(CMAKE_CXX_STANDARD 11)

# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# aux_source_directory(. SRC_LISTS)
# add_executable(planning_main ${SRC_LISTS})

#程序头文件和cpp文件分开时的cmakelists

cmake_minimum_required(VERSION 3.31.0)
project(planning)
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin) #将exe文件和动态库一起放在bin文件下---windows下
#CMAKE_LIBRARY_OUTPUT_DIRECTORY  这是linux下的动态库命令
#CMAKE_ARCHIVE_OUTPUT_DIRECTORY  这是静态库的命令

aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)
add_library(common
SHARED
${SRC_LISTS}
)

target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

add_executable(planning_main planning_main.cpp)

target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include
)

target_link_libraries(planning_main
PUBLIC
common
)
