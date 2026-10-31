add_library(icustubdata STATIC
    stubdata.cpp
)

target_include_directories(icustubdata PRIVATE
    ../common
)

target_compile_definitions(icustubdata PRIVATE
    U_COMMON_IMPLEMENTATION
)
