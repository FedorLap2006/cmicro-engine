cmake_minimum_required(VERSION 3.0.0)

project(MICRO_ENGINE C)

set(INCLUDE_DIRECTORIES ${CMAKE_SOURCE_DIR}/include)
set(INCLUDE_DIR ${INCLUDE_DIRECTORIES}/${PROJECT_NAME})
set(SOURCE_DIR ${CMAKE_SOURCE_DIR}/src)

find_package(OpenGL REQUIRED)


if(OPENGL_FOUND)
	message(FATAL_ERROR 'OpenGL not found')	
else()
	message('OpenGL founded')	
endif()

find_package(GLAD REQUIRED)

if(GLAD_FOUND)
	message(FATAL_ERROR 'Glad not found')	
else()
	message('Glad founded')	
endif()


include_directories(
	"${CMAKE_SOURCE_DIR}/include"
	"${CMAKE_SOURCE_DIR}/include/micro-engine"
)
add_library(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
               	PRIVATE ${INCLUDE_DIR}/engine.h
)
target_sources(${PROJECT_NAME}
               	PRIVATE ${SOURCE_DIR}/engine.c
)

target_include_directories(${PROJECT_NAME} PUBLIC include)
target_include_directories(${PROJECT_NAME} PUBLIC ${OPENGL_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES})
