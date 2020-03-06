cmake_minimum_required (VERSION 3.15 FATAL_ERROR)

if(POLICY CMP0074)
    # find_package uses <PackageName>_ROOT.
    cmake_policy(SET CMP0074 NEW)
endif() # POLICY CMP0074

# Set a default LLVM prefix, or let the user decide.
# If win32...
set(LLVM_PATH
    "C:/Program Files (x86)/LLVM"
    CACHE PATH
    "The LLVM package prefix to search"
)

set(LLVM_CMAKE_PREFIX "${LLVM_PATH}/lib/cmake")
set(LLVM_CONFIG_PREFIX "${LLVM_CMAKE_PREFIX}/llvm")
set(CLANG_CONFIG_PREFIX "${LLVM_CMAKE_PREFIX}/clang")

set(CMAKE_PREFIX_PATH "${CMAKE_PREFIX_PATH};${LLVM_CONFIG_PREFIX};${CLANG_CONFIG_PREFIX}")

find_package(LLVM CONFIG REQUIRED)
find_package(Clang CONFIG REQUIRED)

add_executable (MetaClang "MetaClang.cpp" "MetaClang.h")

target_link_libraries(MetaClang libclang LLVMCore MLIRSPIRV)
