cmake_minimum_required(VERSION 2.8)

project(silicon)

file(READ ${CMAKE_SOURCE_DIR}/client_templates/javascript.js JAVASCRIPT_CLIENT_TEMPLATE)

configure_file(${CMAKE_SOURCE_DIR}/silicon/client_templates/javascript.hh.in
               ${CMAKE_SOURCE_DIR}/silicon/client_templates/javascript.hh)


export(PACKAGE Silicon)

set(SILICON_INCLUDE_DIR "include")
set(CMAKE_CONFIG_DEST "share/silicon")

include(CMakePackageConfigHelpers)
configure_package_config_file (                         
        ${CMAKE_SOURCE_DIR}/SiliconConfig.cmake.in
        ${CMAKE_BINARY_DIR}/SiliconConfig.cmake
        INSTALL_DESTINATION ${CMAKE_CONFIG_DEST}
        PATH_VARS SILICON_INCLUDE_DIR CMAKE_CONFIG_DEST)

configure_file(SiliconConfigVersion.cmake.in
  "${PROJECT_BINARY_DIR}/SiliconConfigVersion.cmake" @ONLY)
#configure_file(SiliconConfig.cmake.in
#  "${PROJECT_BINARY_DIR}/SiliconConfig.cmake" @ONLY)

install(FILES
  "${PROJECT_BINARY_DIR}/SiliconConfig.cmake"
  "${PROJECT_BINARY_DIR}/SiliconConfigVersion.cmake"
  DESTINATION share/silicon)

install(DIRECTORY silicon DESTINATION include
  FILES_MATCHING PATTERN "*.hh")
install(DIRECTORY silicon DESTINATION include
  FILES_MATCHING PATTERN "*.hpp")
