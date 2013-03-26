# NV GLUT paths
SET( CMAKE_INCLUDE_PATH $ENV{NVSDKCOMPUTE_ROOT}/shared/inc )

FIND_PACKAGE(GLUT REQUIRED)
FIND_PACKAGE(OpenGL REQUIRED)
FIND_PACKAGE(GLEW REQUIRED)

IF(WIN32)
		SET( GLUT_LIBRARIES "freeglut.lib")
ENDIF(WIN32)

MESSAGE("GLEW_INCLUDE_PATH = ${GLEW_INCLUDE_PATH}")
configure_file(GLinterop.cl ${CMAKE_CURRENT_BINARY_DIR}/GLinterop.cl COPYONLY)
link_directories(
	${CMAKE_LIBRARY_PATH} 
	${GLEW_LIBRARY_PATH}
	"/usr/local/Cellar/glew/1.9.0/lib"	
)
add_executable( GLinterop GLinterop.cpp )
include_directories( 
    "/usr/include/"
    "/usr/local/include/"
    "/opt/X11/include"
    "/opt/X11/include/freetype2/"
	${GLUT_INCLUDE_DIR} 
	${OPENGL_INCLUDE_DIR} 
	${GLEW_INCLUDE_PATH}
)
target_link_libraries( 
	GLinterop 
	${OPENCL_LIBRARIES} 
	${GLEW_LIBRARIES}
	"-framework OPENCL -framework OPENGL -framework GLUT"
	"-L/usr/local/Cellar/glew/1.9.0/lib -lGLEW"
)

