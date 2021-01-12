cmake_minimum_required(VERSION 3.13)

option(ENABLE_TEST "Enable test program" OFF)
option(ENABLE_TOOL "Enable dump tool" OFF)
option(ENABLE_BINDING_LUA51 "Enable lua 5.1 binding" OFF)
option(ENABLE_BINDING_LUA53 "Enable lua 5.3/5.4 binding" OFF)
project(pbc C)

add_library(libpbc STATIC
  src/context.c
  src/varint.c
  src/array.c
  src/pattern.c
  src/register.c
  src/proto.c
  src/map.c
  src/alloc.c
  src/rmessage.c
  src/wmessage.c
  src/bootstrap.c
  src/stringpool.c
  src/decode.c)
if(WIN32)
  set_target_properties(libpbc PROPERTIES PREFIX "" IMPORT_PREFIX "")
endif()
target_include_directories(libpbc PUBLIC .)

if(ENABLE_TEST)
  add_subdirectory(test)
endif()
if(ENABLE_TOOL)
  add_subdirectory(tool)
endif()
if(ENABLE_BINDING_LUA51)
  add_subdirectory(binding/lua)
endif()
if(ENABLE_BINDING_LUA53)
  add_subdirectory(binding/lua53)
endif()
