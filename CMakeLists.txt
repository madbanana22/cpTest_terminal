cmake_minimum_required (VERSION 3.8)

if (POLICY CMP0141)
	# MSVC hot reload
	cmake_policy(SET CMP0141 NEW)
	set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("cpTest_terminal")

file (GLOB_RECURSE SRCS "src/*.cpp" "src/*.c" "src/*.hpp" "src/*.h") # glob all the source code
# i know its not recommended to do this but idgaf

add_executable (cpTest_terminal ${SRCS}) # remember: frontend is the executable, backend is a library

add_subdirectory (cpTest)

target_link_libraries (cpTest_terminal cpTest)

if (CMAKE_VERSION VERSION_GREATER 3.12)
	# haha cpp version 20 go brbr
	set_property(TARGET cpTest_terminal PROPERTY CXX_STANDARD 20)
endif()