cmake_minimum_required (VERSION 3.0)
project (NanoLog)

# Function to set a compiler flag if it is supported
include(CheckCXXCompilerFlag)
function(enable_cxx_compiler_flag_if_supported flag)
  string(FIND "${CMAKE_CXX_FLAGS}" "${flag}" flag_already_set)
  if(flag_already_set EQUAL -1)
    check_cxx_compiler_flag("${flag}" flag_supported)
    if(flag_supported)
      set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${flag}" PARENT_SCOPE)
    endif()
    unset(flag_supported CACHE)
  endif()
endfunction()

# Set the c++ laguage standard to 14
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


# the library
find_package (Threads)
add_library (NanoLog STATIC NanoLog.cpp)
target_include_directories (NanoLog PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries (NanoLog Threads::Threads)
