CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
SET (CMAKE_VERBOSE_MAKEFILE off)

PROJECT (bluenrg1)
ENABLE_LANGUAGE (ASM-ATT)

INCLUDE_DIRECTORIES("src/")
#INCLUDE_DIRECTORIES("../libmicro/src/")
INCLUDE_DIRECTORIES("${CUBE_ROOT}/Library/hal/inc/")
INCLUDE_DIRECTORIES("${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/inc/")

# +-----------------+
# | My code         |
# +-----------------+
ADD_EXECUTABLE(${CMAKE_PROJECT_NAME}.elf
        "src/Beacon_config.h"
        "src/BLE_Beacon_main.c"
        "src/BlueNRG1_conf.h"
        "src/BlueNRG1_it.c"
        "src/BlueNRG1_it.h"
#        "src/syscalls.c"
)

ADD_DEFINITIONS (-DHS_SPEED_XTAL=HS_SPEED_XTAL_16MHZ -DLS_SOURCE=LS_SOURCE_EXTERNAL_32KHZ -DSMPS_INDUCTOR=SMPS_INDUCTOR_10uH)

# +--------------+
# | STM Cube     |
# +--------------+
add_library ("stm" STATIC

        # Periph
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_adc.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_dma.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_flash.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_gpio.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_i2c.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_mft.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_pka.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_radio.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_rng.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_rtc.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_spi.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_sysCtrl.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_uart.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/BlueNRG1_wdg.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/inc/misc.h"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_adc.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_dma.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_flash.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_gpio.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_i2c.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_mft.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_pka.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_radio.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_rng.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_rtc.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_spi.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_sysCtrl.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_uart.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/BlueNRG1_wdg.c"
        "${CUBE_ROOT}/Library/BlueNRG1_Periph_Driver/src/misc.c"

        # BSP stuff
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/src/SDK_EVAL_Com.c"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/src/SDK_EVAL_Config.c"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/src/SDK_EVAL_Button.c"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/src/SDK_EVAL_Led.c"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/inc/SDK_EVAL_Com.h"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/inc/SDK_EVAL_Config.h"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/inc/SDK_EVAL_Button.h"
        "${CUBE_ROOT}/Library/SDK_Eval_BlueNRG1/inc/SDK_EVAL_Led.h"

        #HAL high level stuff
        "${CUBE_ROOT}/Library/hal/src/osal.c"
        "${CUBE_ROOT}/Library/hal/src/sleep.c"
        "${CUBE_ROOT}/Library/hal/src/context_switch.s"
        "${CUBE_ROOT}/Library/hal/src/clock.c"
        "${CUBE_ROOT}/Library/hal/inc/osal.h"
        "${CUBE_ROOT}/Library/hal/inc/sleep.h"
        "${CUBE_ROOT}/Library/hal/inc/clock.h"

        # Startup code is writen in C for this µC
        "${CUBE_ROOT}/Library/CMSIS/Device/ST/BlueNRG1/Source/system_bluenrg1.c"


        # BLE Stack stuff
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/ble_const.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/ble_status.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/ble_utils.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/bluenrg1_api.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/bluenrg1_events.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/bluenrg1_gap.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/bluenrg1_gatt_server.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/bluenrg1_hal.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/bluenrg1_stack.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/hci_const.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/link_layer.h"
        "${CUBE_ROOT}/Library/Bluetooth_LE/inc/sm.h"

        # CMSIS device specific headers
        "${CUBE_ROOT}/Library/CMSIS/Device/ST/BlueNRG1/Include/BlueNRG1.h"
        "${CUBE_ROOT}/Library/CMSIS/Device/ST/BlueNRG1/Include/BlueNRG_x_device.h"
        "${CUBE_ROOT}/Library/CMSIS/Device/ST/BlueNRG1/Include/system_bluenrg1.h"

        # CMSIS core headers
        "${CUBE_ROOT}/Library/CMSIS/Include/arm_common_tables.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/arm_math.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cm0.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cm0plus.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cm3.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cm4.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cm4_simd.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cmFunc.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_cmInstr.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_sc000.h"
        "${CUBE_ROOT}/Library/CMSIS/Include/core_sc300.h"
)

#set_target_properties (${CMAKE_PROJECT_NAME}.elf PROPERTIES COMPILE_FLAGS "-save-temps")
#TARGET_LINK_LIBRARIES (${CMAKE_PROJECT_NAME}.elf stdc++)
TARGET_LINK_LIBRARIES (${CMAKE_PROJECT_NAME}.elf "${CUBE_ROOT}/Library/Bluetooth_LE/library/libbluenrg1_stack.a")
TARGET_LINK_LIBRARIES (${CMAKE_PROJECT_NAME}.elf "${CUBE_ROOT}/Project/BLE_Examples/BLE_Beacon/TrueSTUDIO/BlueNRG-1/libsmall_printf_atollic.a")
TARGET_LINK_LIBRARIES (${CMAKE_PROJECT_NAME}.elf -Wl,--whole-archive stm -Wl,--no-whole-archive)

ADD_CUSTOM_TARGET(${CMAKE_PROJECT_NAME}.bin ALL DEPENDS ${CMAKE_PROJECT_NAME}.elf COMMAND ${CMAKE_OBJCOPY} -Obinary ${CMAKE_PROJECT_NAME}.elf ${CMAKE_PROJECT_NAME}.bin)

FIND_PROGRAM (ST_FLASH st-flash)
ADD_CUSTOM_TARGET("upload" DEPENDS ${CMAKE_PROJECT_NAME}.elf COMMAND ${ST_FLASH} write ${CMAKE_PROJECT_NAME}.bin 0x8000000)
