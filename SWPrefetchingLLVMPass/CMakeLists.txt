add_library(LLVMSWP MODULE SWPrefetchingLLVMPass.cpp)

target_include_directories(LLVMSWP PRIVATE ${LLVM_INCLUDE_DIRS})
target_compile_definitions(LLVMSWP PRIVATE ${LLVM_DEFINITIONS})
target_compile_options(LLVMSWP PRIVATE -fno-rtti)
