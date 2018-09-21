cmake_minimum_required( VERSION 3.1 )

project( boostdep LANGUAGES CXX )

add_executable( boostdep src/boostdep.cpp )

find_package( Boost COMPONENTS filesystem REQUIRED )
target_link_libraries( boostdep Boost::filesystem )

install( TARGETS boostdep RUNTIME DESTINATION bin )
