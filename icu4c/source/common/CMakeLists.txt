file(STRINGS sources.txt ICU_COMMON_SOURCES)

add_library(icuuc STATIC ${ICU_COMMON_SOURCES})

target_include_directories(icuuc PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_compile_definitions(icuuc PRIVATE U_COMMON_IMPLEMENTATION)
