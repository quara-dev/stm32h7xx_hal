
target = get_option('MCU_FAMILY')
if target.contains('STM32')
        target = target.to_lower()
        message('including @0@ startup files'.format(target))
        # collect sources to compile
        cmsis_device_src =files(
                'system_stm32h7xx_singlecore.c',
                'Source/Templates/gcc/startup_@0@.s'.format(target),
        )
endif
cmsis_device_inc = include_directories(
        'Include'
)

# build_c_flags_hal = '-DSTM32H725xx'

message('cmsis_device: @0@'.format(target))


cmsis_core_dep = dependency('cmsis_core', required: true)


# create HAL lib
lib_cmsis_h7 = static_library(
    'cmsis_h7',
    sources: [
        cmsis_device_src
    ],
    include_directories: [
        cmsis_device_inc
    ],
    dependencies: [
        cmsis_core_dep,
  ],
    c_args: build_c_flags_hal,
)

# create dependencies
lib_cmsis_h7_dep = declare_dependency(
    include_directories: [
        cmsis_device_inc,
    ],
    dependencies: [
        cmsis_core_dep,
   ],
    link_with: lib_cmsis_h7,

)