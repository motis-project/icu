add_executable(genccode
    ../tools/genccode/genccode.c
    ../tools/toolutil/pkg_genc.cpp
    ../tools/toolutil/filestrm.cpp
    ../tools/toolutil/toolutil.cpp
    ../tools/toolutil/uoptions.cpp
)

target_include_directories(genccode PRIVATE ../tools/toolutil/)

target_link_libraries(genccode PRIVATE icuuc)
target_compile_definitions(genccode PRIVATE U_TOOLUTIL_IMPLEMENTATION)

# Update from icu4c-79.1-data-bin-l.zip at https://github.com/unicode-org/icu/releases/
set(ICU_DATA_FILE "${CMAKE_CURRENT_SOURCE_DIR}/in/icudt79l.dat")
set(ICU_DATA_C "${CMAKE_CURRENT_BINARY_DIR}/icudt79l_dat.c")

add_custom_command(
    OUTPUT "${ICU_DATA_C}"
    COMMAND ${CMAKE_CROSSCOMPILING_EMULATOR} $<TARGET_FILE:genccode>
        -e icudt79
        -d "${CMAKE_CURRENT_BINARY_DIR}"
        -f icudt79l_dat
        "${CMAKE_CURRENT_SOURCE_DIR}/in/icudt79l.dat"
    DEPENDS genccode
    VERBATIM
)

add_library(icudata STATIC "${ICU_DATA_C}")
target_include_directories(icudata PRIVATE ../common/)