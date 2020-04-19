set(FILES "${CMAKE_CURRENT_SOURCE_DIR}/header.h")
set(SUBDIRECTORIES "")
set(RELATIVE_PATH "include/CMakeTests")

foreach(VAR ${SUBDIRECTORIES})
add_subdirectory(${VAR})
endforeach()

if(FILES)
	target_sources("${PROJECT_NAME}" PRIVATE ${FILES})
	
	install(FILES ${FILES} DESTINATION ${RELATIVE_PATH})
endif()