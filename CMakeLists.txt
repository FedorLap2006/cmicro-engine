cmake_minimum_required(VERSION 3.0.0)

project(MICRO_ENGINE C)

set(INCLUDE_DIRECTORIES ${CMAKE_SOURCE_DIR}/include)
set(INCLUDE_DIR ${INCLUDE_DIRECTORIES}/micro-engine)
set(SOURCE_DIR ${CMAKE_SOURCE_DIR}/src)

find_package(OpenGL REQUIRED)


if(OPENGL_FOUND)
    message('OpenGL founded')    
else()
    message(FATAL_ERROR 'OpenGL not found')    
endif()

find_package(GLAD REQUIRED)

if(GLAD_FOUND)
    message('Glad founded')    
else()
    message(FATAL_ERROR 'Glad not found')    
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
target_link_libraries(${PROJECT_NAME} PUBLIC ${OPENGL_LIBRARIES})
target_link_libraries(${PROJECT_NAME} PUBLIC glad)