cmake_minimum_required(VERSION 3.23.1)

PROJECT (toupTekX2 LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

add_library(toupTekX2 SHARED 
	Src/main.cpp
	Src/main.h
	Src/x2camera.cpp
	Src/x2Camera.h
)

set_target_properties(toupTekX2 PROPERTIES
  IMPORTED_LOCATION "${CMAKE_SOURCE_DIR}/toupcamsdk/mac/x64+arm64/libtoupcam.dylib"
  INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_SOURCE_DIR}/../../../licensedinterfaces" 
  INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_SOURCE_DIR}toupcamsdk/inc"
)

target_include_directories(toupTekX2 PRIVATE "toupcamsdk/inc")

if(APPLE)
target_link_directories(toupTekX2 PRIVATE "./toupcamsdk/mac/x64+arm64")
endif()

target_compile_definitions(toupTekX2 PRIVATE VK_NO_PROTOTYPES)

#list(APPEND CMAKE_PREFIX_PATH "../../../licensedinterfaces" "./Src")

#link_directories("./toupcamsdk/mac/x64+arm64")
#target_link_libraries(toupTekX2 "libtoupcam.dylib")

