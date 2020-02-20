#project(myapp)
#cmake_minimum_required(VERSION 3.3.2)
#set(CMAKE_SYSTEM_PROCESSOR arm)
#SET(CMAKE_C_COMPILER  aarch64-linux-gnu-gcc)
#SET(CMAKE_CXX_COMPILER  aarch64-linux-gnu-g++)
#set(CMAKE_MODULE_PATH
#    ${CMAKE_MODULE_PATH}
#    "/usr/lib/rti_connext_dds-6.0.0/resource/cmake")
#
#find_package(RTIConnextDDS EXACT "6.0.0" REQUIRED)
#add_executable(${PROJECT_NAME} myapp.c)

cmake_minimum_required(VERSION 3.3.2)
project (example)
set(CMAKE_SYSTEM_PROCESSOR arm)
SET(CMAKE_C_COMPILER  aarch64-linux-gnu-gcc)
SET(CMAKE_CXX_COMPILER  aarch64-linux-gnu-g++)
if(NOT CONNEXTDDS_ARCH)
    message(FATAL_ERROR "You forget the -DCONNEXTDDS_ARCH parameter")
endif()
set(CMAKE_MODULE_PATH
    ${CMAKE_MODULE_PATH}
    "/usr/lib/rti_connext_dds-6.0.0/resource/cmake")

find_package(RTIConnextDDS EXACT "6.0.0" REQUIRED)
include_directories("src" ${CONNEXTDDS_INCLUDE_DIRS})

set(SOURCES_PUB
    HelloWorld_publisher.c
    HelloWorld.c
    HelloWorldPlugin.c
    HelloWorldSupport.c)

add_executable(HelloWorld_c_publisher ${SOURCES_PUB})
target_link_libraries(HelloWorld_c_publisher
    PUBLIC
    RTIConnextDDS::c_api)
