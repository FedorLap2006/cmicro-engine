cmake_minimum_required(VERSION 3.0.0)

project(MICRO_ENGINE C)

set(INCLUDE_DIRECTORIES ${CMAKE_SOURCE_DIR}/include)
set(INCLUDE_DIR ${INCLUDE_DIRECTORIES}/micro-engine)
set(SOURCE_DIR ${CMAKE_SOURCE_DIR}/src)

find_package(OpenGL REQUIRED)


if(OPENGL_FOUND)
    message("[OK] OpenGL founded")    
else()
    message(FATAL_ERROR "[X] OpenGL not found")    
endif()

find_package(GLAD REQUIRED)

if(GLAD_FOUND)
    message("[OK] Glad founded")    
else()
    message(FATAL_ERROR "[X] Glad not found")    
endif()


include_directories(
    "${CMAKE_SOURCE_DIR}/include"
    "${CMAKE_SOURCE_DIR}/include/micro-engine"
)
add_executable(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
                   PRIVATE ${INCLUDE_DIR}/engine.h
)
target_sources(${PROJECT_NAME}
                   PRIVATE ${SOURCE_DIR}/engine.c
                   PRIVATE ${CMAKE_SOURCE_DIR}/main.c
)

target_include_directories(${PROJECT_NAME} PUBLIC include)
target_include_directories(${PROJECT_NAME} PUBLIC ${OPENGL_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} PUBLIC ${OPENGL_LIBRARIES})
target_link_libraries(${PROJECT_NAME} PUBLIC glad)