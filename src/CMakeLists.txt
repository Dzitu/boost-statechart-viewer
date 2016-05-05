cmake_minimum_required(VERSION 3.0)
project (visualizer)
find_package(LLVM REQUIRED CONFIG)
set(LLVM_LINK_COMPONENTS support)
message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

add_definitions(${LLVM_DEFINITIONS} -std=c++11)

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})
link_directories(${LLVM_LIBRARY_DIRS})

add_library(${PROJECT_NAME} MODULE visualizer.cpp)

#llvm_map_components_to_libnames(llvm_libs support core irreader)

target_link_libraries(${PROJECT_NAME}
 clangParse clangFrontend clangSerialization
 clangDriver clangCodeGen clangSema clangAnalysis
 clangAST clangLex clangBasic clangEdit
 ${llvm_libs}
)

