crash_catcher_src = files(
        'Core/src/CrashCatcher_armv7m.S',
        'Core/src/CrashCatcher.c',
)
    
crash_catcher_include = include_directories(
        'include',
        'Core/src',
    )

#--------------------------------------------------------------------
# Compiler flags for ARM builds.
arm_cflags = [
  '-MMD', '-MP',
  '-ffunction-sections', '-fdata-sections', '-fno-exceptions', '-fno-delete-null-pointer-checks', '-fomit-frame-pointer',
  '-std=gnu90'
]
arm_cppflags = arm_cflags + ['-fno-rtti']


crash_catcher = static_library(
    'crash_catcher',
    sources: crash_catcher_src,
    include_directories: crash_catcher_include,
    c_args: [
        arm_cflags,
    ],
    cpp_args: [
        arm_cppflags,
    ],
)
crash_catcher_dep = declare_dependency(
    include_directories: crash_catcher_include,
    include_directories: include_directories(
        'include',
    ),
    link_with: crash_catcher,
    compile_args: [
        '-Wno-switch-default',
    ],
)

