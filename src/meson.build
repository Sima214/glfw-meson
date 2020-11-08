src = [files('context.c', 'init.c', 'input.c', 'monitor.c', 'vulkan.c', 'window.c')]

if wm == 'cocoa'
    src += files('cocoa_init.m', 'cocoa_joystick.m', 'cocoa_monitor.m',
                 'cocoa_window.m', 'cocoa_time.c', 'posix_thread.c',
                 'nsgl_context.m', 'egl_context.c', 'osmesa_context.c')
elif wm == 'win32'
    src += files('win32_init.c', 'win32_joystick.c', 'win32_monitor.c',
                 'win32_time.c', 'win32_thread.c', 'win32_window.c',
                 'wgl_context.c', 'egl_context.c', 'osmesa_context.c')
elif wm == 'x11'
    src += files('x11_init.c', 'x11_monitor.c', 'x11_window.c',
                 'xkb_unicode.c', 'posix_time.c', 'posix_thread.c',
                 'glx_context.c', 'egl_context.c', 'osmesa_context.c')
elif wm == 'wayland'
    src += files('wl_init.c', 'wl_monitor.c', 'wl_window.c',
                 'posix_time.c', 'posix_thread.c', 'xkb_unicode.c',
                 'egl_context.c', 'osmesa_context.c')
elif wm == 'osmesa'
    src += files('null_init.c', 'null_monitor.c', 'null_window.c', 'null_joystick.c',
                 'posix_time.c', 'posix_thread.c', 'osmesa_context.c')
endif

if wm == 'x11' or wm == 'wayland'
    if target_machine.system() == 'linux'
        src += files('linux_joystick.c')
    else
        src += files('null_joystick.c')
    endif
endif

if wm == 'wayland'
    wayland_scanner_executable = find_program('wayland-scanner')
    wayland_protocols_dep = dependency('wayland-protocols', version: '>=1.15')
    wayland_protocols_base = wayland_protocols_dep.get_variable(pkgconfig: 'pkgdatadir')
    wayland_protocols_header_cmd = [wayland_scanner_executable, 'client-header', '@INPUT@', '@OUTPUT@']
    wayland_protocols_code_cmd = [wayland_scanner_executable, 'private-code', '@INPUT@', '@OUTPUT@']
    xdg_shell_xml = join_paths(wayland_protocols_base, 'stable/xdg-shell/xdg-shell.xml')
    xdg_decoration_xml = join_paths(wayland_protocols_base, 'unstable/xdg-decoration/xdg-decoration-unstable-v1.xml')
    viewporter_xml = join_paths(wayland_protocols_base, 'stable/viewporter/viewporter.xml')
    relative_pointer_xml = join_paths(wayland_protocols_base, 'unstable/relative-pointer/relative-pointer-unstable-v1.xml')
    pointer_constraints_xml = join_paths(wayland_protocols_base, 'unstable/pointer-constraints/pointer-constraints-unstable-v1.xml')
    idle_inhibit_xml = join_paths(wayland_protocols_base, 'unstable/idle-inhibit/idle-inhibit-unstable-v1.xml')
    wayland_conv = {
        xdg_shell_xml: 'wayland-xdg-shell-client-protocol',
        xdg_decoration_xml: 'wayland-xdg-decoration-client-protocol',
        viewporter_xml: 'wayland-viewporter-client-protocol',
        relative_pointer_xml: 'wayland-relative-pointer-unstable-v1-client-protocol',
        pointer_constraints_xml: 'wayland-pointer-constraints-unstable-v1-client-protocol',
        idle_inhibit_xml: 'wayland-idle-inhibit-unstable-v1-client-protocol'
    }
    foreach inxml, outfcp: wayland_conv
        wayland_protocol_header = configure_file(command: wayland_protocols_header_cmd, input: files(inxml), output: outfcp + '.h')
        wayland_protocol_source = configure_file(command: wayland_protocols_code_cmd, input: files(inxml), output: outfcp + '.c')
        src += wayland_protocol_source
    endforeach
endif

# TODO: pe dll resource file.

configure_file(input: 'glfw_config.h.in', output: 'glfw_config.h', configuration: glfw_conf, format: 'cmake')

add_project_arguments(ADD_DEFINE_TEMPLATE.format('_GLFW_USE_CONFIG_H'), language: ['c', 'objc'])

glfw_lib = library('glfw', src, 
                   dependencies: [thread_dep, wm_dep, vulkan_dep],
                   build_by_default: false,
                   gnu_symbol_visibility: 'hidden',
                   install: true)
