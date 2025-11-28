# Standard Zephyr Boilerplate
zephyr_library()
zephyr_include_directories(include)

# 1. Calculate path to where source WOULD be if it existed
#    (Standard West layout: workspace/modules/lib/...)
get_filename_component(WEST_TOP "${CMAKE_CURRENT_LIST_DIR}/../../.." ABSOLUTE)
set(PRIVATE_SRC "${WEST_TOP}/modules/lib/test-modem-source")

# 2. Check if source exists
if(EXISTS "${PRIVATE_SRC}/CMakeLists.txt")
    message(STATUS " [TEST] Building from PRIVATE SOURCE")
    add_subdirectory(${PRIVATE_SRC} ${CMAKE_CURRENT_BINARY_DIR}/private_src)
else()
    message(STATUS " [TEST] Linking PUBLIC BINARY")
    # We will add the .a file later
    zephyr_link_libraries(${CMAKE_CURRENT_LIST_DIR}/lib/libmodem_core.a)
endif()