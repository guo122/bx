
set(PROJECT_NAME bx)

set(CMAKE_C_COMPILER g++)
add_compile_options(-std=c++1y)

set(BX_DIR ${CMAKE_CURRENT_SOURCE_DIR})

set(SRCS_PATH
	"include/bx"
	"include/bx/inline"
	"include/tinystl"
	"src"
)

# add platform specific sources
if(OS_IS_WINDOWS)
	set(SRCS_PATH ${SRCS_PATH}
		"include/compat/msvc"
		"include/compat/msvc/pre1600"
	)
elseif(OS_IS_MACOS)
	set(SRCS_PATH ${SRCS_PATH}
		"include/compat/osx"
	)
elseif(OS_IS_IOS)
	set(SRCS_PATH ${SRCS_PATH}
		"include/compat/ios"
	)
endif()		 

set(INC_DIR
	${BX_DIR}/include
	${BX_DIR}/3rdparty
)

IF (OS_IS_WINDOWS)
	set(INC_DIR ${INC_DIR}
		${BX_DIR}/include/compat/msvc
	)
ELSEIF (OS_IS_MACOS)
	set(INC_DIR ${INC_DIR}
		${BX_DIR}/include/compat/osx
	)
ELSEIF (OS_IS_IOS)
	set(INC_DIR ${INC_DIR}
		${BX_DIR}/include/compat/ios
	)
ENDIF()

include_directories(${INC_DIR})

Add_Definitions(-D__STDC_LIMIT_MACROS
				-D__STDC_FORMAT_MACROS
				-D__STDC_CONSTANT_MACROS
				-D_HAS_EXCEPTIONS=0
				-D_HAS_ITERATOR_DEBUGGING=0
				-D_ITERATOR_DEBUG_LEVEL=0
				-D_SCL_SECURE=0
				-D_SECURE_SCL=0
				-D_SCL_SECURE_NO_WARNINGS
				-D_CRT_SECURE_NO_WARNINGS
				-D_CRT_SECURE_NO_DEPRECATE
				-DBX_CONFIG_DEBUG=1
				)

aux_add_lib(
	${PROJECT_NAME} "3rd"
	${SRCS_PATH}
)
