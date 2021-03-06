#
#  Copyright
#


ADD_DEFINITIONS(-DDEBUG=2)
IF(WIN32)
	ADD_DEFINITIONS("-DNOMINMAX")
ENDIF(WIN32)

INCLUDE_DIRECTORIES(${Boost_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR}/include)
LINK_DIRECTORIES(${Boost_LIBRARY_DIRS})

# Static library that will avoid useless recompilation.
add_library(utils STATIC
  gettimeofday.cpp RandomGenerator.cpp
)

# --- tsubmatrix ---
SET(EXECUTABLE_NAME tsubmatrix)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tsubmatrix.cpp)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tbasic ---
SET(EXECUTABLE_NAME tbasic)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tbasic.cpp)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tstage ---
SET(EXECUTABLE_NAME tstage)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tstage.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tdestructiveQR ---
SET(EXECUTABLE_NAME tdestructiveQR)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tdestructiveQR.cpp)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- thcod ---
SET(EXECUTABLE_NAME thcod)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  thcod.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- thcod_full ---
SET(EXECUTABLE_NAME texhcod)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  thcod_full.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
# ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tgivens ---
SET(EXECUTABLE_NAME tgivens)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tgivens.cpp)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tasearch ---
SET(EXECUTABLE_NAME tasearch)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tasearch.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- trandom ---
SET(EXECUTABLE_NAME trandom)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  trandom.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
IF(NOT WIN32)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} ${Boost_PROGRAM_OPTIONS_LIBRARY})
ENDIF(NOT WIN32)
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tcod ---
SET(EXECUTABLE_NAME tcod)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tcod.cpp)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
IF(NOT WIN32)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} ${Boost_PROGRAM_OPTIONS_LIBRARY})
ENDIF(NOT WIN32)
ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

# --- tdamping ---
# SET(EXECUTABLE_NAME tdamping)
# ADD_EXECUTABLE(${EXECUTABLE_NAME}
#   tdamping.cpp)
# ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
# TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
# LIST (APPEND executable_list ${EXECUTABLE_NAME})
# IF(NOT WIN32)
# TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} ${Boost_PROGRAM_OPTIONS_LIBRARY})
# ENDIF(NOT WIN32)

# --- tchrono ---
SET(EXECUTABLE_NAME tchrono)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tchrono.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})

# --- tdump_problem ---
SET(EXECUTABLE_NAME tdump_problem)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  tdump_problem.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})

# --- ttrack ---
SET(EXECUTABLE_NAME ttrack)
ADD_EXECUTABLE(${EXECUTABLE_NAME}
  ttrack.cpp)
ADD_DEPENDENCIES(${EXECUTABLE_NAME} utils)
TARGET_LINK_LIBRARIES(${EXECUTABLE_NAME} utils)
LIST (APPEND executable_list ${EXECUTABLE_NAME})
#ADD_TEST(${EXECUTABLE_NAME} ${EXECUTABLE_NAME})

foreach (exec ${executable_list})
	ADD_DEPENDENCIES(${exec} ${PROJECT_NAME})
	TARGET_LINK_LIBRARIES(${exec} ${PROJECT_NAME})
endforeach(exec)
