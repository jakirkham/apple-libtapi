if(NOT CYGWIN AND NOT MINGW AND NOT WIN32)
  set(LLVM_EXPORTED_SYMBOL_FILE ${CMAKE_CURRENT_SOURCE_DIR}/libtapi.exports)
endif()

add_tapi_library(libtapi
  SHARED
  APIVersion.cpp
  LinkerInterfaceFile.cpp
  Version.cpp
  ${TAPI_CXX_API_HEADERS}

  LINK_LIBS
  tapiCore
  )

set_target_properties(libtapi
  PROPERTIES
  OUTPUT_NAME "tapi"
  )

if(APPLE)
  set_property(TARGET libtapi APPEND_STRING
  PROPERTY
  LINK_FLAGS " -current_version ${TAPI_VERSION_MAJOR}.${TAPI_VERSION_MINOR}.${TAPI_VERSION_PATCH} -compatibility_version 1" # -allowable_client ld"
  )
endif()
