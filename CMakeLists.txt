cmake_minimum_required(VERSION 3.6 FATAL_ERROR)

project(ScintCSU)

find_package(Geant4 REQUIRED ui_all vis_all)

include(${Geant4_USE_FILE})

file(GLOB sources ${PROJECT_SOURCE_DIR}/*.cc)
file(GLOB headers ${PROJECT_SOURCE_DIR}/*.hh)

add_executable(sci main.cc ${sources} ${headers})
target_link_libraries(sci ${Geant4_LIBRARIES})

file(GLOB MACRO_FILES
  "*.mac"
)
file(COPY ${MACRO_FILES} DESTINATION ${PROJECT_BINARY_DIR})

file(GLOB DATA_FILES
  "*.dat"
)
file(COPY ${DATA_FILES} DESTINATION ${PROJECT_BINARY_DIR})

add_custom_target(ScintCSU DEPENDS sci)
