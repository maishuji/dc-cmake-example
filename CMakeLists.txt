cmake_minimum_required(VERSION 3.18.0)

# Avoid warning about DOWNLOAD_EXTRACT_TIMESTAMP in CMake 3.24:
if (CMAKE_VERSION VERSION_GREATER_EQUAL "3.24.0")
    cmake_policy(SET CMP0135 NEW)
endif()
project(dc-make-examples CXX)

# ------------------------------------------ #
# Global cmake variables
# ------------------------------------------ #
set(CMAKE_CXX_STANDARD 20)

# ------------------------------------------ #
# Options
# ------------------------------------------ #


# ------------------------------------------ #
# Cmake modules
# ------------------------------------------ #
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules ${CMAKE_MODULE_PATH})
if(DEFINED PLATFORM_DREAMCAST)
    find_program(CMAKE_CXX_CPPCHECK NAMES cppcheck)
    if(CMAKE_CXX_CPPCHECK)
        message(STATUS " Using cppcheck -------------")
        list(APPEND CMAKE_CXX_CPPCHECK 
            "--enable=all"
            "--suppress=missingIncludeSystem"
            "--suppress=unmatchedSuppression"
            "--suppress=preprocessorErrorDirective"
            "--suppress=syntaxError" 
        )
    endif()
endif(DEFINED PLATFORM_DREAMCAST)

# ------------------------------------------ #
# Subdirectories
# ------------------------------------------ #
add_subdirectory(src)

# ------------------------------------------ #
# Testing
# ------------------------------------------ #
if(NOT DEFINED PLATFORM_DREAMCAST)
    #enable_testing()
    #add_subdirectory(test)
endif()