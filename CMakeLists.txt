cmake_minimum_required(VERSION 3.0)

###############################################################################
# 									miniaudio
###############################################################################
# Project name and version
project(miniaudio LANGUAGES C)
set(MINIAUDIO_VERSION_MAJOR "0")
set(MINIAUDIO_VERSION_MINOR "11")
set(MINIAUDIO_VERSION_REVISION "8")
set(MINIAUDIO_VERSION "${MINIAUDIO_VERSION_MAJOR}.${MINIAUDIO_VERSION_MINOR}.${MINIAUDIO_VERSION_REVISION}")

# Project options
option(MINIAUDIO_BUILD_TESTS "Build the miniaudio tests" OFF)

# Find the library header files
file(GLOB MINIAUDIO_HEADERS "*.h")

# Create the library
add_library(miniaudio INTERFACE)

target_include_directories(miniaudio INTERFACE
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
	$<INSTALL_INTERFACE:include>
)

# Install the library
install(TARGETS miniaudio EXPORT miniaudioTargets
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
	RUNTIME DESTINATION bin
	INCLUDES DESTINATION include
)
install(EXPORT miniaudioTargets
	FILE miniaudioTargets.cmake
	NAMESPACE miniaudio::
	DESTINATION lib/cmake/miniaudio
)
include(CMakePackageConfigHelpers)
write_basic_package_version_file("miniaudioConfigVersion.cmake"
	VERSION ${MINIAUDIO_VERSION}
	COMPATIBILITY SameMajorVersion
)
install(FILES "miniaudioConfig.cmake" "miniaudioConfigVersion.cmake"
	DESTINATION lib/cmake/miniaudio
)

# Create the tests
if(MINIAUDIO_BUILD_TESTS)
	message(FATAL_ERROR "Tests not implemented yet")
endif()

