# SPDX-License-Identifier: Apache-2.0

function(_mbed_get_assembly_k64f)
    if(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
        set(STARTUP_FILE TOOLCHAIN_GCC_ARM/startup_MK64F12.S)
    elseif(${MBED_TOOLCHAIN} STREQUAL "ARM")
        set(STARTUP_FILE TOOLCHAIN_ARM_STD/startup_MK64F12.S)
    elseif(${MBED_TOOLCHAIN} STREQUAL "IAR")
        set(STARTUP_FILE TOOLCHAIN_IAR/startup_MK64F12.S)
    endif()
    target_sources(mbed-core INTERFACE ${STARTUP_FILE})
endfunction()

function(_mbed_set_linker_file)
    if(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
        set(LINKER_FILE ${CMAKE_CURRENT_SOURCE_DIR}/TOOLCHAIN_GCC_ARM/MK64FN1M0xxx12.ld)
    elseif(${MBED_TOOLCHAIN} STREQUAL "ARM")
        set(LINKER_FILE ${CMAKE_CURRENT_SOURCE_DIR}/TOOLCHAIN_ARM_STD/MK64FN1M0xxx12.sct)
    elseif(${MBED_TOOLCHAIN} STREQUAL "IAR")
        set(LINKER_FILE ${CMAKE_CURRENT_SOURCE_DIR}/TOOLCHAIN_IAR/MK64FN1M0xxx12.icf)
    endif()
    set_property(GLOBAL PROPERTY MBED_TARGET_LINKER_FILE ${LINKER_FILE})
endfunction()

_mbed_get_assembly_k64f()
_mbed_set_linker_file()

target_sources(mbed-core
    INTERFACE
        system_MK64F12.c
)

target_include_directories(mbed-core
    INTERFACE
        .
)
