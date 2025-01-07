cmake_minimum_required(VERSION 3.13)

set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_VERSION 1)

set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-eabi-g++)
set(CMAKE_ASM_COMPILER  arm-none-eabi-gcc)
set(CMAKE_AR arm-none-eabi-ar)
set(CMAKE_OBJCOPY arm-none-eabi-objcopy)
set(CMAKE_OBJDUMP arm-none-eabi-objdump)
set(SIZE arm-none-eabi-size)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 11)

# 设置 PATH 环境变量
set(ENV{PATH} "$ENV{PATH};${CMAKE_CURRENT_SOURCE_DIR}/picotool")
set(ENV{PICO_SDK_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/pico-sdk")

# 设置默认值
set(PICO_PLATFORM "rp2350" CACHE STRING "Target platform for the Pico project")

# 打印变量以确保正确
message(STATUS "PICO_PLATFORM: ${PICO_PLATFORM}")

include("$ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake")

project(Pico-Template C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_executable(Pico-Template
        src/main.c
        )

target_link_libraries(Pico-Template pico_stdlib)

#pico_enable_stdio_usb(Pico-Template 1)
pico_enable_stdio_uart(Pico-Template 1)

pico_add_extra_outputs(Pico-Template)
