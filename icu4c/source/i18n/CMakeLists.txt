file(STRINGS sources.txt ICU_SOURCES)

add_library(icui18n STATIC ${ICU_SOURCES})

target_include_directories(icui18n PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../common
)

target_compile_definitions(icui18n PRIVATE U_I18N_IMPLEMENTATION)

target_link_libraries(icui18n PUBLIC icuuc icudata)
