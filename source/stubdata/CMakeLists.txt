add_library(icustubdata stubdata.cpp)

if(U_USING_ICU_NAMESPACE)
  target_compile_definitions(icustubdata PUBLIC U_USING_ICU_NAMESPACE=1)
else()
  target_compile_definitions(icustubdata PUBLIC U_USING_ICU_NAMESPACE=0)
endif()

if(NOT BUILD_SHARED_LIBS)
  if(MSVC)
    target_compile_definitions(icustubdata PUBLIC U_STATIC_IMPLEMENTATION)
  else()
    target_compile_definitions(icustubdata PUBLIC $<BUILD_INTERFACE:U_STATIC_IMPLEMENTATION>)
  endif()
endif()

target_include_directories(
    icustubdata
    PRIVATE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/../common>
)

if(ICU_DATA_ARCHIVE_MODE)
  install(
      TARGETS icustubdata
      EXPORT "${TARGETS_EXPORT_NAME}"
      LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
      ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
      RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
      INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
  )
endif()

# Name expected by Boost
if(MSVC)
  set(output_name icudt)
else()
  set(output_name icudata)
endif()

set_target_properties(
    icustubdata
    PROPERTIES
    EXPORT_NAME data
    OUTPUT_NAME ${output_name}
)
