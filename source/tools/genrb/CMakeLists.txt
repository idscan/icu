add_executable(
    genrb
    errmsg.c
    errmsg.h
    filterrb.cpp
    filterrb.h
    genrb.cpp
    genrb.h
    parse.cpp
    parse.h
    prscmnts.cpp
    prscmnts.h
    rbutil.c
    rbutil.h
    read.c
    read.h
    reslist.cpp
    reslist.h
    rle.c
    rle.h
    ustr.c
    ustr.h
    wrtjava.cpp
    wrtxml.cpp
)

target_link_libraries(genrb PUBLIC icutu icui18n icuuc)

install(
    TARGETS genrb
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

if(ICU_BUILD_IO)
  add_executable(derb derb.cpp)

  target_link_libraries(derb PUBLIC icuio icutu icui18n icuuc)

  install(
      TARGETS derb
      EXPORT "${TARGETS_EXPORT_NAME}"
      LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
      ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
      RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
      INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
  )
endif()
