cmake_minimum_required(VERSION 3.22)
project(apt-get)

set(LLVM_ROOT "/home/tako/prog/pgsp/llvm-10" CACHE PATH "Root of LLVM install.")

# A bit of a sanity check :
if(NOT EXISTS ${LLVM_ROOT}/include/llvm)
  message(FATAL_ERROR
    "LLVM_ROOT (${LLVM_ROOT}) is invalid ")
endif()

list(APPEND CMAKE_PREFIX_PATH
  "${LLVM_ROOT}/share/llvm/cmake ")
find_package(LLVM REQUIRED CONFIG)


list(APPEND CMAKE_MODULE_PATH "${LLVM_CMAKE_DIR}")
include(HandleLLVMOptions) # load additional config
include(AddLLVM) # used to add our own modules

# See commit r197394, needed by add_llvm_module in llvm/CMakeLists .txt
set(LLVM_RUNTIME_OUTPUT_INTDIR "${CMAKE_BINARY_DIR}/bin/${CMAKE_CFG_INT_DIR}")
set(LLVM_LIBRARY_OUTPUT_INTDIR "${CMAKE_BINARY_DIR}/lib/${CMAKE_CFG_INT_DIR}")

add_subdirectory(SWPrefetchingLLVMPass)
