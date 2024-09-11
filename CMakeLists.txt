cmake_minimum_required(VERSION 3.27)
project(easy-profiler VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(easy-profiler INTERFACE)

target_include_directories(easy-profiler
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/easy-profiler>
)

target_link_directories(easy-profiler
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib>
  $<INSTALL_INTERFACE:lib/easy-profiler>
)

target_link_libraries(easy-profiler
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib/easy_profiler.lib>
  $<INSTALL_INTERFACE:easy_profiler.lib>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/easy-profilerConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/easy-profilerConfig.cmake"
  INSTALL_DESTINATION share/easy-profiler
)

install(TARGETS easy-profiler
  EXPORT easy-profilerTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/include/easy"
  DESTINATION include/easy-profiler
)

install(FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/easy_profiler.lib"
  DESTINATION lib/easy-profiler
)

install(FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/bin/easy_profiler.dll"
  DESTINATION bin
)

install(
  EXPORT easy-profilerTargets
  DESTINATION share/easy-profiler
  NAMESPACE easy-profiler::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/easy-profilerConfig.cmake"
  DESTINATION share/easy-profiler
)