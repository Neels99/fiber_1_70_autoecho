set(TARGET_NAME autoecho)

set(${TARGET_NAME}_SRC ${TARGET_NAME}.cpp)

add_executable(${TARGET_NAME} ${${TARGET_NAME}_SRC})

target_link_libraries(${TARGET_NAME} ${TARGET_LIB}
    boost_thread
    boost_system
    boost_chrono
    boost_coroutine
    boost_context
    boost_fiber
    boost_filesystem
    pthread
    atomic
    )
