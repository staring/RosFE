
include_directories(${REACTOS_SOURCE_DIR}/include/reactos/wine)
add_definitions(-D__WINESRC__)
spec2def(traffic.dll traffic.spec)

list(APPEND SOURCE
    traffic_main.c
    ${CMAKE_CURRENT_BINARY_DIR}/traffic_stubs.c
    ${CMAKE_CURRENT_BINARY_DIR}/traffic.def)

add_library(traffic SHARED ${SOURCE})
set_module_type(traffic win32dll)
target_link_libraries(traffic wine)
add_importlibs(traffic msvcrt kernel32 ntdll)
add_cd_file(TARGET traffic DESTINATION reactos/system32 FOR all)
