project(
    'stm32h7xx_hal_driver',
    'c',
    default_options: [
        'warning_level=1',
        'werror=false',
        'b_staticpic=false',
        'c_std=gnu11',
        'build.c_std=gnu11',
        'b_colorout=always',
        'b_lto=true',
    ],
    version: 'v1.11.5',
    meson_version: '>=1.3.0',
    license: 'MIT',
)

assert(
    meson.is_cross_build(),
    'STM32 Hal lib can only be built in a cross build environment.',
)
cc = meson.get_compiler('c')


add_project_arguments(
    [
        '-Wno-implicit-fallthrough',
        '-Wno-missing-prototypes',
        '-Wno-unused-parameter',
        '-Wno-redundant-decls',
        '-Wno-sign-conversion',
        '-Wno-switch-enum',
        '-Wno-return-type',
        '-Wno-pedantic',
        '-Wno-comment',
        '-Wno-error',
    ],
    native: false,
    language: 'c',
)

cmsis_dsp_include = include_directories('cmsis_core/DSP/Include')
cmsis_core_include = include_directories('cmsis_core/Include')



cmsis_core_dep = declare_dependency(
  dependencies: cc.find_library(
    'arm_cortexM7lfdp_math',
    dirs: [meson.current_source_dir() + '/cmsis_core/DSP/Lib/GCC/'],
  ),
  include_directories: [cmsis_core_include, cmsis_dsp_include],
  compile_args: [
    '-DARM_MATH_CM7',
  ],
)


target_mcu = get_option('MCU_FAMILY')


subdir('Stm32Hal')


build_c_flags_hal += [ '-DUSE_HAL_DRIVER', '-DUSE_FULL_LL_DRIVER']


configure_file(
    input: 'config/stm32h7xx_hal_conf.h.in',
    output: 'stm32h7xx_hal_conf.h',
    configuration: stm32h7_hal_config,
)


# create HAL lib
libstm32hal = static_library(
    'stm32_hal',
    sources: [
        stm32_h7_ss.all_sources()
    ],
    include_directories: [
        stm32h7xx_hal_driver_include
    ],
    dependencies: [
        cmsis_h7_dep,
        crash_catcher_dep.as_link_whole(),
    ],
    c_args: build_c_flags_hal,
)

# create dependencies
libstm32hal_dep = declare_dependency(
    include_directories: [
        stm32h7xx_hal_driver_include,
    ],
    dependencies: [
        cmsis_h7_dep,        
        crash_catcher_dep.as_link_whole(),
    ],
    link_with: libstm32hal,

)
