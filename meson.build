project('GLFW', ['c'], version: '3.4.0', 
        default_options : [
            'c_std=c99',
            'buildtype=debugoptimized',
            'warning_level=1',
            'default_library=static'
        ])

ADD_DEFINE_TEMPLATE = '-D@0@'
ADD_DEFINE_VALUE_TEMPLATE = '-D@0@=@1@'

compiler = meson.get_compiler('c')

export_defs = []

if get_option('default_library') == 'shared' or get_option('default_library') == 'both'
    add_project_arguments(ADD_DEFINE_TEMPLATE.format('_GLFW_BUILD_DLL'), language: ['c'])
    export_defs += ADD_DEFINE_TEMPLATE.format('GLFW_DLL')
endif

glfw_conf = configuration_data()
if get_option('GLFW_USE_HYBRID_HPG')
    glfw_conf.set10('_GLFW_USE_HYBRID_HPG', true)
endif

thread_dep = dependency('threads')

# Detect and select backend APIs
if get_option('GLFW_USE_WAYLAND')
    message('Using Wayland for window creation')
    wm = 'wayland'
    glfw_conf.set10('_GLFW_WAYLAND', true)
    wayland_client_dep = dependency('wayland-client', version: '>=0.2.7')
    wayland_cursor_dep = dependency('wayland-cursor', version: '>=0.2.7')
    wayland_egl_dep = dependency('wayland-egl', version: '>=0.2.7')
    wayland_xkb_dep = dependency('xkbcommon')
    if compiler.check_header('xkbcommon/xkbcommon-compose.h', dependencies: wayland_xkb_dep)
        glfw_conf.set10('HAVE_XKBCOMMON_COMPOSE_H', true)
    endif
    if compiler.has_function('memfd_create')
        glfw_conf.set10('HAVE_MEMFD_CREATE', true)
    endif
    # TODO: EpollShim on non-linux unix
    wm_dep = declare_dependency(dependencies: [
        wayland_client_dep, wayland_cursor_dep, wayland_egl_dep, wayland_xkb_dep
    ])
elif get_option('GLFW_USE_OSMESA')
    # TODO: Using OSMesa for headless context creation
    glfw_conf.set10('_GLFW_OSMESA', true)
elif target_machine.system() == 'windows'
    message('Using Win32 for window creation')
    wm = 'win32'
    glfw_conf.set10('_GLFW_WIN32', true)
    wm_dep = declare_dependency()
    add_project_arguments(ADD_DEFINE_TEMPLATE.format('_UNICODE'), language: ['c'])
    add_project_arguments(ADD_DEFINE_TEMPLATE.format('UNICODE'), language: ['c'])
    add_project_arguments(ADD_DEFINE_TEMPLATE.format('_CRT_SECURE_NO_WARNINGS'), language: ['c'])
    add_project_arguments(ADD_DEFINE_VALUE_TEMPLATE.format('WINVER', '0x0501'), language: ['c'])
    if not compiler.check_header('dinput.h')
        error('DirectX 9 headers not found; install DirectX 9 SDK')
    endif
elif target_machine.system() == 'darwin'
    message('Using Cocoa for window creation')
    wm = 'cocoa'
    glfw_conf.set10('_GLFW_COCOA', true)
    wm_dep = declare_dependency(link_args: ['-framework Cocoa', '-framework IOKit', '-framework CoreFoundation'])
elif target_machine.system() == 'linux'
    message('Using X11 for window creation')
    wm = 'x11'
    glfw_conf.set10('_GLFW_X11', true)
    x11_dep = dependency('X11')
    if not compiler.check_header('X11/extensions/Xrandr.h', dependencies: x11_dep)
        error('RandR headers not found; install libxrandr development package')
    endif
    if not compiler.check_header('X11/extensions/Xinerama.h', dependencies: x11_dep)
        error('Xinerama headers not found; install libxinerama development package')
    endif
    if not compiler.check_header('X11/extensions/XKB.h', dependencies: x11_dep)
        error('XKB headers not found; install X11 development package')
    endif
    if not compiler.check_header('X11/Xcursor/Xcursor.h', dependencies: x11_dep)
        error('Xcursor headers not found; install libxcursor development package')
    endif
    if not compiler.check_header('X11/extensions/XInput.h', dependencies: x11_dep)
        error('XInput headers not found; install libxi development package')
    endif
    if not compiler.check_header('X11/extensions/shape.h', dependencies: x11_dep)
        error('X Shape headers not found; install libxext development package')
    endif
    wm_dep = x11_dep
else
    error('No supported platform was detected')
endif

# Add the Vulkan loader as a dependency if necessary
if get_option('GLFW_VULKAN_STATIC')
    glfw_conf.set10('_GLFW_VULKAN_STATIC', true)
    vulkan_dep = dependency('vulkan')
else
    vulkan_dep = declare_dependency()
endif

# TODO: install config.

# Add subdirectories
subdir('include')
subdir('src')

if get_option('GLFW_BUILD_EXAMPLES')
    subdir('examples')
endif

if get_option('GLFW_BUILD_TESTS')
    subdir('tests')
endif

if get_option('GLFW_BUILD_DOCS')
    subdir('docs')
endif
