# Start of root CMakeLists.txt

cmake_minimum_required(VERSION 3.10)

project(hello_world VERSION 0.1 LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# List of components
set(COMPONENTS 
  )

add_executable(hello_world main.cpp)
target_compile_features(hello_world PRIVATE cxx_std_17)

if(MSVC)
        target_compile_options(hello_world PRIVATE /W4)
else()
        target_compile_options(hello_world PRIVATE -Wall -Wextra)
endif()

# Add component subdirectories using loop
foreach(COMPONENT ${COMPONENTS})
    add_subdirectory(components/${COMPONENT})
endforeach()

# Linking to coverage report tool in case of test build
if(CMAKE_BUILD_TYPE MATCHES Test)
    target_link_libraries(hello_world gcov)
endif()

# End of root CMakeLists.txt
