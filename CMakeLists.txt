cmake_minimum_required(VERSION 2.8)

PROJECT(portplay)

if(WIN32)
  # nothing to do?
elseif(APPLE)
  include_directories(/usr/local/include/oscpack ${CMAKE_SOURCE_DIR}/../oscpack)
  link_directories(/usr/local/lib)
  set(CMAKE_CXX_FLAGS "-g -Wall")
  set(CMAKE_C_FLAGS "-g -Wall")
else()
  include_directories(/usr/include/oscpack)
  include_directories(/usr/local/include/oscpack)
  link_directories(/usr/local/lib)
  set(CMAKE_CXX_FLAGS "-g -Wall")
  set(CMAKE_C_FLAGS "-g -Wall")
endif()

# Prefer static lib if available
find_library(OSCPACK NAMES liboscpack.a oscpack PATHS ${CMAKE_SOURCE_DIR}/../oscpack)

add_executable(sendosc sendosc.cpp)
target_link_libraries(sendosc ${OSCPACK})

INSTALL(TARGETS sendosc RUNTIME DESTINATION bin)

