
if target_mcu.contains('STM32')
        target_mcu = target_mcu.to_lower()
        message('including @0@ startup files'.format(target_mcu))
        # collect sources to compile
        cmsis_device_src =files(
                'system_stm32h7xx_singlecore.c',
                'gcc/startup_@0@.s'.format(target_mcu),
        )
endif
cmsis_device_inc = include_directories(
        'Include'
)

manipulate_target_mcu = target_mcu.to_upper()
new_target_mcu = manipulate_target_mcu.replace('XX', 'xx')
message('cmsis_device: @0@'.format(new_target_mcu))

build_c_flags_hal = ['-D'+new_target_mcu]



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
cmsis_h7_dep = declare_dependency(
    include_directories: [
        cmsis_device_inc,
    ],
    dependencies: [
        cmsis_core_dep,
   ],
    link_with: lib_cmsis_h7,

)