# SPDX-License-Identifier: MIT

if(OQS_ENABLE_KEM_frodokem_640_aes)
    set(SRCS kem_frodokem640aes.c external/frodo640aes.c)
endif()
if(OQS_ENABLE_KEM_frodokem_640_shake)
    set(SRCS ${SRCS} kem_frodokem640shake.c external/frodo640shake.c)
endif()

if(OQS_ENABLE_KEM_frodokem_976_aes)
    set(SRCS ${SRCS} kem_frodokem976aes.c external/frodo976aes.c)
endif()
if(OQS_ENABLE_KEM_frodokem_976_shake)
    set(SRCS ${SRCS} kem_frodokem976shake.c external/frodo976shake.c)
endif()

if(OQS_ENABLE_KEM_frodokem_1344_aes)
    set(SRCS ${SRCS} kem_frodokem1344aes.c external/frodo1344aes.c)
endif()
if(OQS_ENABLE_KEM_frodokem_1344_shake)
    set(SRCS ${SRCS} kem_frodokem1344shake.c external/frodo1344shake.c)
endif()

add_library(frodokem OBJECT ${SRCS})

if(OQS_USE_AVX2_INSTRUCTIONS)
    if(OQS_USE_AES_INSTRUCTIONS)
        if(OQS_ENABLE_KEM_frodokem_640_aes)
            set(SRCS_AVX2 external/frodo640aes_avx2.c)
        endif()
        if(OQS_ENABLE_KEM_frodokem_976_aes)
            set(SRCS_AVX2 ${SRCS_AVX2} external/frodo976aes_avx2.c)
        endif()
        if(OQS_ENABLE_KEM_frodokem_1344_aes)
            set(SRCS_AVX2 ${SRCS_AVX2} external/frodo1344aes_avx2.c)
        endif()
    endif()
    if(OQS_ENABLE_KEM_frodokem_640_shake)
        set(SRCS_AVX2 ${SRCS_AVX2} external/frodo640shake_avx2.c)
    endif()
    if(OQS_ENABLE_KEM_frodokem_976_shake)
        set(SRCS_AVX2 ${SRCS_AVX2} external/frodo976shake_avx2.c)
    endif()
    if(OQS_ENABLE_KEM_frodokem_1344_shake)
        set(SRCS_AVX2 ${SRCS_AVX2} external/frodo1344shake_avx2.c)
    endif()

    add_library(frodokem_avx2 OBJECT ${SRCS_AVX2})
    target_compile_options(frodokem_avx2 PRIVATE -maes -mavx2)
endif()
