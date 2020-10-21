add_library(
    icutu
    collationinfo.cpp
    collationinfo.h
    dbgutil.cpp
    dbgutil.h
    denseranges.cpp
    denseranges.h
    filestrm.cpp
    filestrm.h
    filetools.cpp
    filetools.h
    flagparser.cpp
    flagparser.h
    package.cpp
    package.h
    pkg_genc.cpp
    pkg_genc.h
    pkg_gencmn.cpp
    pkg_gencmn.h
    pkg_icu.cpp
    pkg_icu.h
    pkg_imp.h
    pkgitems.cpp
    ppucd.cpp
    ppucd.h
    swapimpl.cpp
    swapimpl.h
    toolutil.cpp
    toolutil.h
    ucbuf.cpp
    ucbuf.h
    ucln_tu.cpp
    ucm.cpp
    ucm.h
    ucmstate.cpp
    udbgutil.cpp
    udbgutil.h
    unewdata.cpp
    unewdata.h
    uoptions.cpp
    uoptions.h
    uparse.cpp
    uparse.h
    writesrc.cpp
    writesrc.h
    xmlparser.cpp
    xmlparser.h
)

target_compile_definitions(icutu PRIVATE U_TOOLUTIL_IMPLEMENTATION)

target_link_libraries(icutu PUBLIC icuuc icui18n)

if(U_HAVE_ELF_H)
  target_compile_definitions(icutu PUBLIC U_HAVE_ELF_H=1)
endif()

target_include_directories(
    icutu
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
)

install(
    TARGETS icutu
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

set_target_properties(icutu PROPERTIES EXPORT_NAME tu)
