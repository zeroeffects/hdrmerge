cmake_minimum_required(VERSION 2.6)

#install(FILES data/cameras.xml data/showcameras.xsl DESTINATION ${SHARE_INSTALL}/hdrmerge/rawspeed)

FILE(GLOB RAWSPEED_SOURCES RawSpeed/*.cpp)
LIST(REMOVE_ITEM RAWSPEED_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/RawSpeed/RawSpeed.cpp")
message(STATUS ${RAWSPEED_SOURCES})

#
# build librawspeed
#
if(WIN32)
  set(RAWSPEED_LIBS "msvcrt")
  add_definitions("-DNO_PTHREAD")
else(WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
endif(WIN32)

add_definitions(-D_UNICODE -DUNICODE)

add_library(rawspeed STATIC ${RAWSPEED_SOURCES})

target_link_libraries(rawspeed ${RAWSPEED_LIBS})
