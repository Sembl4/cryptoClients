cmake_minimum_required(VERSION 3.12)
project(test_clients)

set(CMAKE_CXX_STANDARD 20)

# Flags
if(CMAKE_BUILD_TYPE MATCHES "Debug")
	add_definitions(-DDEBUG)
elseif(CMAKE_BUILD_TYPE MATCHES "Release")
	add_definitions(-DRELEASE)
endif()

if(CMAKE_OPTIMIZE MATCHES "O3")
	set(CMAKE_CXX_FLAGS_RELEASE "-O3")
	set(CMAKE_CXX_FLAGS "-O3")
elseif(CMAKE_OPTIMIZE MATCHES "O2")
	set(CMAKE_CXX_FLAGS_RELEASE "-O2")
	set(CMAKE_CXX_FLAGS "-O2")
elseif(CMAKE_OPTIMIZE MATCHES "O1")
	set(CMAKE_CXX_FLAGS_RELEASE "-O1")
	set(CMAKE_CXX_FLAGS "-O1")
elseif(CMAKE_OPTIMIZE MATCHES "None")
endif()

set(CMAKE_INTERPROCEDURAL_OPTIMIZATION TRUE)

add_definitions(-DTIMESTAMP)

add_subdirectory(lib)

find_package(OpenSSL REQUIRED)

include_directories(
    /usr/local/include
    /usr/local/include/hv
    ${OPENSSL_INCLUDE_DIR}
    ${PROJECT_SOURCE_DIR}/lib
)

add_executable(${PROJECT_NAME} tests.cpp)

target_link_libraries(${PROJECT_NAME} PRIVATE
    Client
    /usr/local/lib/libhv.a
    ${OPENSSL_LIBRARIES}
)
target_link_directories(${PROJECT_NAME} PUBLIC
    "${PROJECT_BINARY_DIR}"
    "${PROJECT_SOURCE_DIR}/lib"
    "${CMAKE_CURRENT_SOURCE_DIR}/lib"
)