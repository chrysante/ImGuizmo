cmake_minimum_required(VERSION 3.23)

set(CMAKE_CXX_STANDARD 20)

#option(IMGUIZMO_IMGUI_INCLUDEDIR "ImGui include directory")

project(
  imguizmo
  VERSION 0.0.0
  DESCRIPTION ""
  LANGUAGES CXX)

add_library(ImGuizmo STATIC)

target_include_directories(ImGuizmo
  PUBLIC
    include
)

target_sources(ImGuizmo
  PRIVATE
    include/ImGuizmo/ImGuizmo.h
    src/ImGuizmo.cpp
)

if(PROJECT_IS_TOP_LEVEL)
  file(
    DOWNLOAD
    https://github.com/cpm-cmake/CPM.cmake/releases/download/v0.38.3/CPM.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/cmake/CPM.cmake
    EXPECTED_HASH SHA256=cc155ce02e7945e7b8967ddfaff0b050e958a723ef7aad3766d368940cb15494
  )
  include(${CMAKE_CURRENT_BINARY_DIR}/cmake/CPM.cmake)
  CPMAddPackage("gh:chrysante/imgui#docking")
  message("Setting IMGUIZMO_IMGUI_INCLUDEDIR")
  set(IMGUIZMO_IMGUI_INCLUDEDIR ${imgui_SOURCE_DIR})
endif()

target_include_directories(ImGuizmo PRIVATE ${IMGUIZMO_IMGUI_INCLUDEDIR})