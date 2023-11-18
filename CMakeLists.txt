# Copyright 2018 Mike Dev
# Copyright 2018 Peter Dimov
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at http://www.boost.org/LICENSE_1_0.txt

cmake_minimum_required( VERSION 3.5...3.28 )

project( boostdep LANGUAGES CXX )

option( BOOSTDEP_USE_STD_FS "Use std::filesystem instead of boost::filesystem" OFF )

add_executable( boostdep src/boostdep.cpp )

if( BOOSTDEP_USE_STD_FS )

    message(STATUS "Using std::filesystem as filesystem library")

    target_compile_definitions( boostdep PUBLIC BOOSTDEP_USE_STD_FS )
    target_compile_features( boostdep PUBLIC cxx_std_17 )

    # NOTE: Some compilers (e.g. g++-8) will require additional linker flags
    #        in order to use std::filesystem (e.g. -lstdc++fs).
    #        We are NOT handling those special cases

else()

    message(STATUS "Using Boost::filesystem as filesystem library")

    find_package( Boost COMPONENTS filesystem REQUIRED )
    target_link_libraries( boostdep PUBLIC Boost::filesystem )

endif()

install( TARGETS boostdep RUNTIME DESTINATION bin )
