cmake_minimum_required (VERSION 2.8)

project(jsoncpp CXX)

set(vendor "${CMAKE_CURRENT_SOURCE_DIR}/..")
include(${vendor}/unifier/unifier.cmake)

set(libname "jsoncpp")
set(libtype STATIC)

if (MSVC)
	add_definitions("/wd4251")
	add_definitions(-DJSON_DLL_BUILD)
endif()

set(src
	"src/lib_json/json_reader.cpp"
	"src/lib_json/json_value.cpp"
	"src/lib_json/json_writer.cpp")

set(hdr
	"src/lib_json/json_batchallocator.h"
	"src/lib_json/json_tool.h")

set(public_hdr
	"include/json/assertions.h"
	"include/json/autolink.h"
	"include/json/config.h"
	"include/json/features.h"
	"include/json/forwards.h"
	"include/json/json.h"
	"include/json/reader.h"
	"include/json/value.h"
	"include/json/writer.h")

include_directories(include)

add_library(${libname} ${libtype} ${src} ${hdr} ${public_hdr})
set_target_properties(${libname} PROPERTIES PUBLIC_HEADER "${public_hdr}")
target_link_libraries(${libname} ${platformlibs})

install(TARGETS ${libname}
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
	PUBLIC_HEADER DESTINATION include/json)
