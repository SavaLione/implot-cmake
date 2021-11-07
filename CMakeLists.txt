#################################################################################
# Copyright (c) 2021, Savely Pototsky (SavaLione)
# All rights reserved.
#################################################################################
# Checking the minimum version
cmake_minimum_required (VERSION 3.13.1)

# Project name
set(IMPLOT_PROJECT "implot")
set(IMPLOT_PROJECT_VERSION "0.13")

project(${IMPLOT_PROJECT}
    VERSION ${IMPLOT_PROJECT_VERSION}
    LANGUAGES CXX
)

#################################################################################
#                                     Options                                   #
#################################################################################
option(IMPLOT_BUILD_STATIC "Build static library" OFF)

#################################################################################
#                                      Implot                                   #
#################################################################################

set(IMPLOT_SRC
    src/implot.cpp
    src/implot_demo.cpp
    src/implot_items.cpp
)

# implot
if(IMPLOT_BUILD_STATIC)
    add_library(${IMPLOT_PROJECT} STATIC ${IMPLOT_SRC})
else()
    add_library(${IMPLOT_PROJECT} SHARED ${IMPLOT_SRC})
endif()

if (NOT TARGET imgui)
    add_subdirectory(${PROJECT_SOURCE_DIR}/lib/imgui)
endif()

target_link_libraries(${IMPLOT_PROJECT} imgui)
target_include_directories(${IMPLOT_PROJECT} PUBLIC ${PROJECT_SOURCE_DIR}/include)