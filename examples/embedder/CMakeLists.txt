find_package(WaylandEGL REQUIRED)
find_package(WPE-mesa REQUIRED)

set(WPE_EMBEDDER_DIR "${TOOLS_DIR}/wpe/examples/embedder")

set(WPE_EMBEDDER_SOURCES
    ${WPE_EMBEDDER_DIR}/main.cpp
)

set(WPE_EMBEDDER_INCLUDE_DIRECTORIES
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/Source
    ${FORWARDING_HEADERS_DIR}
    ${WPE_MESA_INCLUDE_DIRS}
    ${WTF_DIR}
)

set(WPE_EMBEDDER_SYSTEM_INCLUDE_DIRECTORIES
    ${GLIB_INCLUDE_DIRS}
    ${WAYLAND_EGL_INCLUDE_DIRS}
)

set(WPE_EMBEDDER_LIBRARIES
    WebKit2
    wayland-client
    ${WAYLAND_EGL_LIBRARIES}
    ${GLIB_LIBRARIES}
    ${WPE_MESA_LIBRARIES}
)

include_directories(SYSTEM ${WPE_EMBEDDER_SYSTEM_INCLUDE_DIRECTORIES})
add_executable(WPEEmbedder ${WPE_EMBEDDER_SOURCES})
target_include_directories(WPEEmbedder PUBLIC ${WPE_EMBEDDER_INCLUDE_DIRECTORIES})
target_link_libraries(WPEEmbedder ${WPE_EMBEDDER_LIBRARIES})
install(TARGETS WPEEmbedder DESTINATION "${EXEC_INSTALL_DIR}")
