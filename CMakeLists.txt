#  _               _ 
# | |__   _____  _(_)
# | '_ \ / _ \ \/ / | MIT & Apache 2.0 dual licensed
# | | | |  __/>  <| | Version 1.3.5
# |_| |_|\___/_/\_\_| https://github.com/EmberEmu/hexi

cmake_minimum_required(VERSION 3.29)

set(HEXI_PROJECT_NAME hexi)

project(${HEXI_PROJECT_NAME}
	VERSION 1.3.5
	LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED OFF)
set(CMAKE_CXX_EXTENSIONS OFF)

option(ENABLE_TESTING OFF)

##############################
#         Google Test        #
##############################

if(ENABLE_TESTING)
	find_package(Threads REQUIRED)
    include(FetchContent)

    FetchContent_Declare(
      googletest
      URL https://github.com/google/googletest/releases/download/v1.16.0/googletest-1.16.0.tar.gz
      URL_HASH SHA512=bec8dad2a5abbea8e9e5f0ceedd8c9dbdb8939e9f74785476b0948f21f5db5901018157e78387e106c6717326558d6642fc0e39379c62af57bf1205a9df8a18b 
    )

    # For Windows: Prevent overriding the parent project's compiler/linker settings
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
    FetchContent_MakeAvailable(googletest)
    set(FETCHCONTENT_FULLY_DISCONNECTED ON)

    include(GoogleTest)

    set(cmake_ctest_arguments "CTEST_OUTPUT_ON_FAILURE")
    enable_testing()
    add_subdirectory(tests)
endif()

##############################
#       Library Target       #
##############################

add_library(${HEXI_PROJECT_NAME} INTERFACE)
add_library(${HEXI_PROJECT_NAME}::${HEXI_PROJECT_NAME} ALIAS ${HEXI_PROJECT_NAME})

target_include_directories(${HEXI_PROJECT_NAME} INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

add_subdirectory(include)

target_sources(${HEXI_PROJECT_NAME} INTERFACE
	FILE_SET HEADERS
    BASE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/include
    FILES ${HEXI_HEADERS}
)

##############################
#       Library Install      #
##############################

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

install(TARGETS ${HEXI_PROJECT_NAME}
	EXPORT ${HEXI_PROJECT_NAME}-targets
	FILE_SET HEADERS
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/${HEXI_PROJECT_NAME}-config.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/${HEXI_PROJECT_NAME}-config.cmake"
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${HEXI_PROJECT_NAME}
)

write_basic_package_version_file(
	"${CMAKE_CURRENT_BINARY_DIR}/${HEXI_PROJECT_NAME}-config-version.cmake"
	VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion
)

install(
	FILES
		"${CMAKE_CURRENT_BINARY_DIR}/${HEXI_PROJECT_NAME}-config.cmake"
		"${CMAKE_CURRENT_BINARY_DIR}/${HEXI_PROJECT_NAME}-config-version.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${HEXI_PROJECT_NAME}
)

install(EXPORT ${HEXI_PROJECT_NAME}-targets
	NAMESPACE ${HEXI_PROJECT_NAME}::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${HEXI_PROJECT_NAME}
)

install(FILES
	"${CMAKE_CURRENT_SOURCE_DIR}/LICENSE"
	"${CMAKE_CURRENT_SOURCE_DIR}/LICENSE-MIT"
	"${CMAKE_CURRENT_SOURCE_DIR}/README.md"
	DESTINATION ${CMAKE_INSTALL_DOCDIR}
    OPTIONAL
)