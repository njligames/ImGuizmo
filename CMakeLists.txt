cmake_minimum_required(VERSION 3.5.1)

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
if(BUILD_SHARED_LIB)
  ADD_LIBRARY(ImGuizmo SHARED ${imgui_SRCS} ${imgui_HDRS})
endif()

if(BUILD_STATIC_LIB)
  ADD_LIBRARY(ImGuizmo STATIC ${imgui_SRCS} ${imgui_HDRS})
endif()
 
install (TARGETS ImGuizmo DESTINATION ${CMAKE_INSTALL_LIBDIR})
install (FILES ImGuizmo.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

foreach(p LIB INCLUDE)
    set(var CMAKE_INSTALL_${p}DIR)
    if(NOT IS_ABSOLUTE "${${var}}")
        set(${var} "${CMAKE_INSTALL_PREFIX}/${${var}}")
    endif()
endforeach()
