cmake_minimum_required(VERSION 3.0)
project(Box2D)

option(BUILD_SHARED_LIBRARY "Build shared library" ON)
option(BUILD_EXAMPLE_PROGRAM "Build HelloWorld"	OFF)

file(GLOB sources
	Box2D.h
	Box2D/Collision/*.cpp
	Box2D/Collision/*.h
	Box2D/Collision/Shapes/*.cpp
	Box2D/Collision/Shapes/*.h	
	Box2D/Common/*.cpp
	Box2D/Common/*.h
	Box2D/Dynamics/Joints/*.cpp
	Box2D/Dynamics/Joints/*.h
	Box2D/Dynamics/Contacts/*.cpp
	Box2D/Dynamics/Contacts/*.h
	Box2D/Dynamics/*.cpp
	Box2D/Dynamics/*.h
	Box2D/Rope/*.cpp
	Box2D/Rope/*.h
)

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	Box2D
	Box2D/Collision
	Box2D/Collision/Shapes
	Box2D/Common/
	Box2D/Dynamics/Joints
	Box2D/Dynamics/Contacts
	Box2D/Dynamics
	Box2D/Rope
)

if (BUILD_SHARED_LIBRARY)
	set(BUILD_TYPE	SHARED)
else()
	set(BUILD_TYPE	STATIC)
endif()

add_library(Box2D ${BUILD_TYPE} ${sources})

target_compile_options(Box2D PUBLIC -std=c++11)

if (BUILD_EXAMPLE_PROGRAM)
	add_executable(Box2D_HelloWorld HelloWorld/HelloWorld.cpp)
	target_link_libraries(Box2D_HelloWorld Box2D)
endif()

# Install library
install(TARGETS Box2D DESTINATION lib)

# Install library headers
file(GLOB HEADERS Box2D/Box2D.h)
install(FILES ${HEADERS} DESTINATION include)
