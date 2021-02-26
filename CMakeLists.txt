cmake_minimum_required(VERSION 3.14)
project(rabbitmq-example CXX)
# include(ExternalProject))

#         ExternalProject_Add(
#                 rabbitmq-c
#                 GIT_REPOSITORY https://github.com/alanxz/rabbitmq-c.git
#                 GIT_TAG        "b8e5f43b082c5399bf1ee723c3fd3c19cecd843e"
#                 GIT_SHALLOW    1
#                 CMAKE_ARGS "-DENABLE_SSL_SUPPORT=OFF -DBUILD_TOOLS=OFF -DBUILD_DOCS=OFF"
#              )
include(FetchContent)
FetchContent_Declare(
        rabbitmq-c
        GIT_REPOSITORY https://github.com/alanxz/rabbitmq-c.git
        GIT_TAG        "b8e5f43b082c5399bf1ee723c3fd3c19cecd843e"
        GIT_SHALLOW    1
        PREFIX          3rdparty
        CMAKE_ARGS "-DENABLE_SSL_SUPPORT=OFF -DBUILD_TOOLS=OFF -DBUILD_DOCS=OFF"
        )

option(BUILD_TOOLS "" OFF)
option(ENABLE_SSL_SUPPORT "" OFF)
option(BUILD_SHARED_LIBS "" OFF)
option(BUILD_STATIC_LIBS "" ON)
option(BUILD_EXAMPLES  "" OFF)
option(BUILD_TOOLS "" OFF)
option(BUILD_TOOLS_DOCS  "" OFF)
option(BUILD_TESTS "" OFF)
option(BUILD_API_DOCS "" OFF)
option(RUN_SYSTEM_TESTS  "" OFF)

#FetchContent_MakeAvailable(rabbitmq-c)
FetchContent_GetProperties(rabbitmq-c)
if(NOT rabbitmq-c_POPULATED)
    FetchContent_Populate(rabbitmq-c)
    add_subdirectory(${rabbitmq-c_SOURCE_DIR} ${rabbitmq-c_BINARY_DIR} )
    add_library(rabbitmqc ALIAS rabbitmq-static)
    set(RMQ_INCLUDES_DIR ${rabbitmq-c_SOURCE_DIR}/librabbitmq)
endif()

add_executable(${PROJECT_NAME} main.cpp)
set_target_properties(${PROJECT_NAME} PROPERTIES CXX_STANDARD 17)
target_link_libraries(${PROJECT_NAME}  rabbitmq-static)
target_include_directories(${PROJECT_NAME} PUBLIC ${RMQ_INCLUDES_DIR})
