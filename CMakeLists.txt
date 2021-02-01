project(fiber_boost)
cmake_minimum_required(VERSION 3.18)
set(CMAKE_CXX_STANDARD 20)

set(TARGET_NAME autoecho)

set(${TARGET_NAME}_SRC ${TARGET_NAME}.cpp)

set(Boost_USE_STATIC_LIBS ON)

set(Boost_DEBUG ON)
set(Boost_VERBOSE ON)
set(Boost_USE_DEBUG_LIBS         ON) # ignore debug libs and

find_package(Boost 1.74.0 COMPONENTS thread system chrono coroutine context fiber filesystem REQUIRED)
set(PROJECT_LIB ${PROJECT_LIB} ${Boost_LOG_LIBRARY} ${Boost_LOG_SETUP_LIBRARY})
include_directories(${Boost_INCLUDE_DIRS})
if(Boost_FOUND)
	MESSAGE( STATUS "Boost_INCLUDE_DIRS = ${Boost_INCLUDE_DIRS}.")
    MESSAGE( STATUS "Boost_LIBRARIES = ${BOOST_LIBRARYDIR}.")
    MESSAGE( STATUS "Boost_LIB_VERSION = ${Boost_LIB_VERSION}.")
endif()
    

add_executable(${TARGET_NAME} ${${TARGET_NAME}_SRC})

if(WIN32)
    target_link_libraries(${PROJ_NAME} ws2_32) #возник баг, без этого не компилится boost код.
    target_link_libraries(${PROJ_NAME} wsock32) #возник баг, без этого не компилится boost код.
endif()

target_link_libraries(${TARGET_NAME} ${TARGET_LIB}
    Boost::thread
    Boost::system
    Boost::chrono
    Boost::coroutine
    Boost::context
    Boost::fiber
    Boost::filesystem
    pthread
    atomic
    )
