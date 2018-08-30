cmake_minimum_required (VERSION 3.6)
project("Sample Unity with cmake" C)

set(TARGET_GROUP test CACHE STRING "Group to build") # set the target group to be either test or production

# Add the modules that exist in both our release and our unit tests
add_subdirectory(module_a)

if(TARGET_GROUP STREQUAL production)
    message(">>> building application for production")
    add_subdirectory(main)
elseif(TARGET_GROUP STREQUAL test)
    message(">>> building application for testing")
    include(CTest) # let the Ctest module of CMake know about we are about to test

    # add the
    add_subdirectory(unity)
    add_subdirectory(test)
else()
    message(FATAL_ERROR "Given TARGET_GROUP unknown")
endif()
