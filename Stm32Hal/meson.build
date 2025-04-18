
subdir('helper')
subdir('cmsis-device')

setmod = import('sourceset')
fs = import('fs')
stm32_h7_ss = setmod.source_set()

# Create configuration data object
stm32h7_hal_config = configuration_data()
message('Configuring STM32H7 HAL library')

stm32h7xx_hal_driver_include = include_directories('.', 'Inc', 'Inc/Legacy')

# add sources
stm32_h7_ss.add(
    files(
        'Src/stm32h7xx_hal.c',
        'Src/stm32h7xx_hal_pwr.c',
        'Src/stm32h7xx_hal_pwr_ex.c',
        'Src/stm32h7xx_hal_rcc.c',
        'Src/stm32h7xx_hal_rcc_ex.c',
        'Src/stm32h7xx_hal_exti.c',
        'Src/stm32h7xx_hal_crc.c',
        'Src/stm32h7xx_hal_crc_ex.c',
        'Src/stm32h7xx_hal_gpio.c',
        
        
        # Actually used by HAL
        'Src/stm32h7xx_ll_delayblock.c', # Actually used by HAL
        'Src/stm32h7xx_ll_exti.c',
        'Src/stm32h7xx_ll_crc.c',
        'Src/stm32h7xx_ll_pwr.c',
        'Src/stm32h7xx_ll_rcc.c', # Actually used by HAL
        'Src/stm32h7xx_ll_usb.c',
        'Src/stm32h7xx_ll_utils.c',
        'Src/stm32h7xx_ll_gpio.c',

    ),
)

# set default peripheral enabled
stm32h7_hal_config.set('HAL_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_CORTEX_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_DMA_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_FLASH_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_GPIO_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_HSEM_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_EXTI_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_MDMA_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_PWR_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_RCC_MODULE_ENABLED', true)
stm32h7_hal_config.set('HAL_CRC_MODULE_ENABLED', true)

all_peripherals = [
    'CEC',
    'COMP',
    'CORDIC',
    'ADC',
    'CRYP',
    'DAC',
    'DCMI',
    'DFSDM',
    'DMA2D',
    'DTS',
    'DSI',
    'ETH',
    'FDCAN',
    'GFXMMU',
    'FMAC',
    'HASH',
    'HCD',
    'HRTIM',
    'I2C',
    'I2S',
    'IRDA',
    'IWDG',
    'JPEG',
    'LPTIM',
    'LTDC',
    'MDIOS',
    'MMC',
    'NAND',
    'NOR',
    'OPAMP',
    'OSPI',
    'OTFDEC',
    'PCD',
    'PSSI',
    'QSPI',
    'RAMECC',
    'RNG',
    'RTC',
    'SAI',
    'SD',
    'SDIO',
    'SDRAM',
    'SMARTCARD',
    'SMBUS',
    'SPDIFRX',
    'SPI',
    'SRAM',
    'SWPMI',
    'TIM',
    'UART',
    'USART',
    'WWDG',
]
# enable HAL components
# set options
foreach hal_peripheral : all_peripherals
    hal_option = 'ENABLE_' + hal_peripheral
    hal_module = 'HAL_@0@_MODULE_ENABLED'.format(hal_peripheral.to_upper())
    src_file_hal = 'Src/stm32h7xx_hal_@0@.c'.format(hal_peripheral.to_lower())
    src_file_ex_hal = 'Src/stm32h7xx_hal_@0@_ex.c'.format(hal_peripheral.to_lower())
    src_file_ll = 'Src/stm32h7xx_ll_@0@.c'.format(hal_peripheral.to_lower())
    if get_option(hal_option)
        stm32h7_hal_config.set(hal_module, true)
        if fs.exists(src_file_hal)
        # message(src_file_hal)
        stm32_h7_ss.add(files(src_file_hal))
        endif
        if fs.exists(src_file_ex_hal)
            stm32_h7_ss.add(files(src_file_ex_hal))
        endif
        if fs.exists(src_file_ll)
            stm32_h7_ss.add(files(src_file_ll))
        endif
    else
        stm32h7_hal_config.set(hal_module, false)
    endif
endforeach

stm32h7_hal_config.set('HAL_MODULE_ENABLED', true)
stm32h7_hal_config.set('VDD_VALUE', get_option('MCU_VDD'))
stm32h7_hal_config.set('HSE_VALUE', get_option('MCU_HSE_VALUE'))
stm32h7_hal_config.set('HSI_VALUE', get_option('MCU_HSI_VALUE'))
stm32h7_hal_config.set('CSI_VALUE', get_option('MCU_CSI_VALUE'))
stm32h7_hal_config.set('LSE_VALUE', get_option('MCU_LSE_VALUE'))
stm32h7_hal_config.set('LSI_VALUE', get_option('MCU_LSI_VALUE'))

