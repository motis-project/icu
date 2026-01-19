file(STRINGS sources.txt ICU_SOURCES)

add_library(icui18n STATIC ${ICU_SOURCES})

target_include_directories(icui18n SYSTEM PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../common
)

target_compile_definitions(icui18n PRIVATE U_I18N_IMPLEMENTATION)

if (MSVC)
    target_compile_options(icui18n PRIVATE /utf-8)
endif()

target_link_libraries(icui18n PUBLIC icuuc icudata)
