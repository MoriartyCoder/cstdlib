cmake_minimum_required(VERSION 3.10)
project(cstdlib VERSION 1.0 LANGUAGES C)

file(GLOB_RECURSE SOURCES "src/*.c")

add_library(cstdlib SHARED ${SOURCES})

target_include_directories(cstdlib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

if(MSVC)
	target_compile_options(cstdlib PRIVATE /W4)
else()
	target_compile_options(cstdlib PRIVATE -Wall -Wextra -O2)
endif()

set_target_properties(cstdlib PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)


install(TARGETS cstdlib
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
	RUNTIME DESTINATION bin)

install(DIRECTORY include/ DESTINATION include)

