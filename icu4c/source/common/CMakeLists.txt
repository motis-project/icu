file(STRINGS sources.txt ICU_COMMON_SOURCES)

add_library(icuuc STATIC ${ICU_COMMON_SOURCES})

target_include_directories(icuuc SYSTEM PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

if (MSVC)
    target_compile_options(icuuc PRIVATE /utf-8)
endif()

target_compile_definitions(icuuc PRIVATE U_COMMON_IMPLEMENTATION)
target_compile_definitions(icuuc PUBLIC U_STATIC_IMPLEMENTATION)
