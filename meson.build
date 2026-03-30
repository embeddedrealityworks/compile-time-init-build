project(
    'cib',
    'cpp',
    version: '0.1.0',
    license: 'BSL-1.0',
    meson_version: '>=1.1.0',
    default_options: [
        'cpp_std=c++23',
        'warning_level=3',
    ],
    description: 'A header-only C++ library for composing modular firmware at compile-time.',
)

cib_inc = include_directories('include')

# --- Dependencies from subprojects ---

stdx_proj        = subproject('cpp-std-extensions')
stdx_dep         = stdx_proj.get_variable('stdx_dep')

mp11_proj        = subproject('mp11')
mp11_dep         = mp11_proj.get_variable('mp11_dep')

fmt_proj         = subproject('fmt')
fmt_dep          = fmt_proj.get_variable('fmt_dep')

concurrency_proj = subproject('cpp-baremetal-concurrency')
concurrency_dep  = concurrency_proj.get_variable('concurrency_dep')

async_proj       = subproject('cpp-baremetal-senders-and-receivers')
async_dep        = async_proj.get_variable('async_dep')

# --- Sub-library declarations (all header-only) ---

cib_match_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [stdx_dep],
)

cib_interrupt_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [mp11_dep, concurrency_dep, stdx_dep],
)

cib_lookup_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [stdx_dep],
)

cib_log_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [stdx_dep],
)

cib_nexus_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [stdx_dep],
)

cib_msg_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [async_dep, mp11_dep, cib_log_dep, cib_lookup_dep, cib_match_dep, stdx_dep],
)

cib_log_fmt_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [cib_log_dep, fmt_dep, stdx_dep],
)

cib_log_binary_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [cib_log_dep, cib_msg_dep, concurrency_dep, stdx_dep],
)

cib_flow_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [mp11_dep, cib_log_dep, cib_nexus_dep, stdx_dep],
)

cib_seq_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [cib_flow_dep, cib_log_dep, cib_nexus_dep, stdx_dep],
)

# Omnibus dependency — pulls in everything
cib_dep = declare_dependency(
    include_directories: cib_inc,
    dependencies: [
        cib_flow_dep,
        cib_interrupt_dep,
        cib_log_dep,
        cib_log_binary_dep,
        cib_log_fmt_dep,
        cib_lookup_dep,
        cib_match_dep,
        cib_msg_dep,
        cib_nexus_dep,
        cib_seq_dep,
        stdx_dep,
    ],
)

meson.override_dependency('cib', cib_dep)
meson.override_dependency('cib_match', cib_match_dep)
meson.override_dependency('cib_interrupt', cib_interrupt_dep)
meson.override_dependency('cib_lookup', cib_lookup_dep)
meson.override_dependency('cib_log', cib_log_dep)
meson.override_dependency('cib_nexus', cib_nexus_dep)
meson.override_dependency('cib_msg', cib_msg_dep)
meson.override_dependency('cib_log_fmt', cib_log_fmt_dep)
meson.override_dependency('cib_log_binary', cib_log_binary_dep)
meson.override_dependency('cib_flow', cib_flow_dep)
meson.override_dependency('cib_seq', cib_seq_dep)
