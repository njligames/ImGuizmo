cmake_minimum_required(VERSION 3.7)

# add the binary tree directory to the search path 
# for include files
include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/../imgui )
 
SET(imgui_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/imgui.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/imgui_demo.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/imgui_draw.cpp
    )

SET(imgui_HDRS
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/imgui.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/imgui_internal.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/imconfig.h 
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/stb_rect_pack.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/stb_textedit.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../imgui/stb_truetype.h
    )

# add the binary tree directory to the search path 
# for include files
include_directories( ${CMAKE_CURRENT_SOURCE_DIR} )
 
SET(ImGuizmo_SRCS
    ${imgui_SRCS}
    ${CMAKE_CURRENT_SOURCE_DIR}/ImGuizmo.cpp
    )

SET(ImGuizmo_HDRS
    ${imgui_HDRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/ImGuizmo.h
    )

# add the main library
add_library(ImGuizmo ${ImGuizmo_SRCS} ${ImGuizmo_HDRS})
 
install (TARGETS ImGuizmo DESTINATION ${CMAKE_INSTALL_LIBDIR})
install (FILES ImGuizmo.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

foreach(p LIB INCLUDE)
    set(var CMAKE_INSTALL_${p}DIR)
    if(NOT IS_ABSOLUTE "${${var}}")
        set(${var} "${CMAKE_INSTALL_PREFIX}/${${var}}")
    endif()
endforeach()
