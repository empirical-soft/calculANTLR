cmake_minimum_required(VERSION 3.5)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

# C++14
set(CMAKE_CXX_STANDARD 14)

# set-up ANTLR
add_definitions(-DANTLR4CPP_STATIC)
set(ANTLR_EXECUTABLE ${PROJECT_SOURCE_DIR}/thirdparty/antlr/antlr-4.7.2-complete.jar)
set(ANTLR4_ZIP_REPOSITORY ${PROJECT_SOURCE_DIR}/thirdparty/antlr/antlr4-master.zip)
include(ExternalAntlr4Cpp)
include_directories(${ANTLR4_INCLUDE_DIRS})

# generate ANTLR files
find_package(ANTLR REQUIRED)
antlr_target(Calculantlr
    ${CMAKE_CURRENT_SOURCE_DIR}/src/Calculantlr.g4
    PACKAGE calculantlr
    VISITOR)
include_directories(${ANTLR_Calculantlr_OUTPUT_DIR})

# generate ASDL files
find_package(ASDL)
ASDL_TARGET(AST ${CMAKE_CURRENT_SOURCE_DIR}/src/AST.asdl
    ${CMAKE_CURRENT_BINARY_DIR}/AST.h
    ${CMAKE_CURRENT_BINARY_DIR}/AST.cpp)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

# build calculantlr
file(GLOB CALCULANTLR_SRC "src/*.cpp")
include_directories(${PROJECT_SOURCE_DIR}/thirdparty)
add_executable(calculantlr ${CALCULANTLR_SRC}
    ${ANTLR_Calculantlr_CXX_OUTPUTS}
    ${ASDL_AST_OUTPUTS})
target_link_libraries(calculantlr antlr4_static)

