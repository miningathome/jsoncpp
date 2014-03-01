cmake_minimum_required (VERSION 2.8)

project(jsoncpp CXX)

include(cmake/clean_slate.cmake)

set(libname "jsoncpp")

set(libtype STATIC)

set(src
	"dist/jsoncpp.cpp")

set(public_hdr
	"dist/json/json.h"
	"dist/json/json-forwards.h")

include_directories(dist)

add_library(${libname} ${libtype} ${src} ${public_hdr})
set_target_properties(${libname} PROPERTIES PUBLIC_HEADER "${public_hdr}")
target_link_libraries(${libname} ${platformlibs})

install(TARGETS ${libname}
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
	PUBLIC_HEADER DESTINATION include/json)