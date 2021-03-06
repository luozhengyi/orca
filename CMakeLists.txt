CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT(orca)
SET(VERSION 1.0.0)


SET(LIB_DIRECTORY
    ${PROJECT_SOURCE_DIR}/uv-cpp/libuv1.30.0/lib/gcc8.3.0/)

SET(SOURCE_DIRECTORY
    ${PROJECT_SOURCE_DIR}/uv-cpp/uv/
    ${PROJECT_SOURCE_DIR}/uv-cpp/uv/http/
    ${PROJECT_SOURCE_DIR}/src/orca/base/condition/
    ${PROJECT_SOURCE_DIR}/src/orca/base/error/
    ${PROJECT_SOURCE_DIR}/src/orca/base/queue/
    ${PROJECT_SOURCE_DIR}/src/orca/base/SpinLock/
    ${PROJECT_SOURCE_DIR}/src/orca/base/thread/
    ${PROJECT_SOURCE_DIR}/src/orca/core/
    ${PROJECT_SOURCE_DIR}/src/orca/core/net/
    )
    
SET(INCLUDE_DIRECTORY
    ${PROJECT_SOURCE_DIR}/uv-cpp/libuv1.30.0/include/
    ${PROJECT_SOURCE_DIR}/
    )
    
SET(OUTPUT_DIR 
    "${PROJECT_SOURCE_DIR}/orca_lib")


SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c11 -m64 -O2")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -m64 -O2")


INCLUDE_DIRECTORIES(${INCLUDE_DIRECTORY})

FOREACH(SOURCE_DIR ${SOURCE_DIRECTORY})
    AUX_SOURCE_DIRECTORY(${SOURCE_DIR} SOURCES)
ENDFOREACH()

SET(OUTPUT_SHARED "${PROJECT_NAME}_shared")
SET(OUTPUT_STATIC "${PROJECT_NAME}_static")

LINK_DIRECTORIES(LIB_DIRECTORY)
TARGET_LINK_LIBRARIES(${PROJECT_SHARED} "libuv.a")
TARGET_LINK_LIBRARIES(${PROJECT_STATIC} "libuv.a")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/orca_lib")

ADD_LIBRARY (${OUTPUT_SHARED} SHARED ${SOURCES} )
ADD_LIBRARY (${OUTPUT_STATIC} STATIC ${SOURCES} )

#SET_TARGET_PROPERTIES(${OUTPUT_STATIC} PROPERTIES  LIBRARY_OUTPUT_DIRECTORY "${OUTPUT_DIR}" )

#SET_TARGET_PROPERTIES(${OUTPUT_SHARED} PROPERTIES  LIBRARY_OUTPUT_DIRECTORY "${OUTPUT_DIR}" )
