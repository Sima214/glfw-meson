clipboard_exe = executable('clipboard', 'clipboard.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
events_exe = executable('events', 'events.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
msaa_exe = executable('msaa', 'msaa.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
glfwinfo_exe = executable('glfwinfo', 'glfwinfo.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib, gladvulkan_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
iconify_exe = executable('iconify', 'iconify.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
monitors_exe = executable('monitors', 'monitors.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
reopen_exe = executable('reopen', 'reopen.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')
cursor_exe = executable('cursor', 'cursor.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    win_subsystem: 'console')

win32entry = []
if target_machine.system() == 'windows'
    win32entry += '/ENTRY:mainCRTStartup'
endif

empty_exe = executable('empty', 'empty.c',
    include_directories: dep_inc,
    link_with: [tinycthread_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
gamma_exe = executable('gamma', 'gamma.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
icon_exe = executable('icon', 'icon.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
inputlag_exe = executable('inputlag', 'inputlag.c',
    include_directories: dep_inc,
    link_with: [getopt_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
joysticks_exe = executable('joysticks', 'joysticks.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
tearing_exe = executable('tearing', 'tearing.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
threads_exe = executable('threads', 'threads.c',
    include_directories: dep_inc,
    link_with: [tinycthread_lib, gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
timeout_exe = executable('timeout', 'timeout.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
title_exe = executable('title', 'title.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
triangle_vulkan_exe = executable('triangle-vulkan', 'triangle-vulkan.c',
    include_directories: dep_inc,
    link_with: [gladvulkan_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
window_exe = executable('window', 'window.c',
    include_directories: dep_inc,
    link_with: [gladgl_lib],
    dependencies: [thread_dep, glfw_dep],
    link_args: win32entry,
    win_subsystem: 'windows')
