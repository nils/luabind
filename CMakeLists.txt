# Copyright (C) 2007-2009 LuaDist.
# Modified by Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.
# Original build script by Leandro Motta Barros.

	PROJECT(luabind)
	CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
	INCLUDE(dist.cmake)

# Find Lua
	FIND_PACKAGE(Lua51 REQUIRED)

# Find Boost
	SET(Boost_USE_STATIC_LIBS OFF)
#~ 	FIND_PACKAGE(Boost 1.38 COMPONENTS unit_test_framework REQUIRED)
	FIND_PACKAGE(Boost 1.38  REQUIRED)

# Include directories
	INCLUDE_DIRECTORIES(${Boost_INCLUDE_DIRS} ${LUA_INCLUDE_DIR} ${CMAKE_CURRENT_SOURCE_DIR})

# Link directories
#~ 	LINK_DIRECTORIES(${BOOST_LIBRARY_DIRS})

# Build the library
	SET(LUABIND_SRC src/class.cpp src/class_info.cpp src/class_registry.cpp src/class_rep.cpp src/create_class.cpp src/error.cpp src/exception_handler.cpp src/function.cpp src/inheritance.cpp src/link_compatibility.cpp src/object_rep.cpp src/open.cpp src/pcall.cpp src/scope.cpp src/stack_content_by_name.cpp src/weak_ref.cpp src/wrapper_base.cpp)

	ADD_DEFINITIONS(-DLUABIND_BUILDING)

	ADD_LIBRARY(luabind SHARED ${LUABIND_SRC})
	TARGET_LINK_LIBRARIES(luabind ${LUA_LIBRARIES})

#~ 2TODO: Tests

# Add CTest support
#~ 	ENABLE_TESTING()

# Unit tests
#~ 	FUNCTION(AddUnitTest name)
#~ 		ADD_EXECUTABLE(${name} Tests/${name}.cpp)
#~ 		TARGET_LINK_LIBRARIES(${name} ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY} ${LUA_LIBRARIES} diluculum)
#~ 		ADD_TEST(${name} ${name})
#~ 	ENDFUNCTION(AddUnitTest)

#~ 	ADD_LIBRARY(ATestModule SHARED Tests/ATestModule.cpp)
#~ 	TARGET_LINK_LIBRARIES(ATestModule diluculum ${LUA_LIBRARIES})
#~ 	SET_TARGET_PROPERTIES(ATestModule PROPERTIES PREFIX "")

#~ 	AddUnitTest(TestLuaFunction)

# Build examples
#~ 	FUNCTION(AppExample name sources includes)
#~ 		INCLUDE_DIRECTORIES(${includes})
#~ 		ADD_EXECUTABLE(${name} ${sources})
#~ 		TARGET_LINK_LIBRARIES(${name} luabind)
#~ 	ENDFUNCTION(AppExample)

#~ 	AppExample(any_converter "examples/any_converter/any_converter.cpp" "" )
#~ 	AppExample(filesystem "examples/filesystem/filesystem.cpp" "examples/filesystem" )
#~ 	AppExample(glut "examples/glut/glut_bind.cpp" "" )
#~ 	AppExample(hello_world "examples/hello_world/hello_world.cpp" "" )
#~ 	AppExample(intrusive_ptr "examples/intrusive_ptr/intrusive_ptr.cpp" "" )
#~ 	AppExample(regexp "examples/regexp/regex_wrap.cpp" "" )

# Install
	INSTALL(TARGETS luabind RUNTIME DESTINATION ${INSTALL_BIN} LIBRARY DESTINATION ${INSTALL_LIB} ARCHIVE DESTINATION ${INSTALL_LIB})	
	INSTALL(DIRECTORY luabind DESTINATION ${INSTALL_INC})
	INSTALL(FILES LICENSE INSTALL DESTINATION ${INSTALL_DATA})
	INSTALL(DIRECTORY doc/ DESTINATION ${INSTALL_DOC})
	


