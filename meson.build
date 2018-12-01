project('Yadifmod', 'cpp',
  default_options : ['buildtype=release', 'b_ndebug=if-release', 'cpp_std=c++14'],
  meson_version : '>=0.48.0',
  version : '10'
)

add_project_arguments('-ffast-math', language : 'cpp')

sources = [
  'Yadifmod/Yadifmod.cpp',
  'Yadifmod/vectorclass/instrset.h',
  'Yadifmod/vectorclass/instrset_detect.cpp'
]

vapoursynth_dep = dependency('vapoursynth').partial_dependency(compile_args : true, includes : true)

libs = []

if host_machine.cpu_family().startswith('x86')
  add_project_arguments('-DVS_TARGET_CPU_X86', '-mfpmath=sse', '-msse2', language : 'cpp')

  sources += [
    'Yadifmod/Yadifmod_SSE2.cpp',
    'Yadifmod/vectorclass/vectorclass.h',
    'Yadifmod/vectorclass/vectorf128.h',
    'Yadifmod/vectorclass/vectorf256.h',
    'Yadifmod/vectorclass/vectorf256e.h',
    'Yadifmod/vectorclass/vectori128.h',
    'Yadifmod/vectorclass/vectori256.h',
    'Yadifmod/vectorclass/vectori256e.h'
  ]

  libs += static_library('avx', 'Yadifmod/Yadifmod_AVX.cpp',
    dependencies : vapoursynth_dep,
    cpp_args : ['-mavx'],
    gnu_symbol_visibility : 'hidden'
  )

  libs += static_library('avx2', 'Yadifmod/Yadifmod_AVX2.cpp',
    dependencies : vapoursynth_dep,
    cpp_args : ['-mavx2', '-mfma'],
    gnu_symbol_visibility : 'hidden'
  )
endif

shared_module('yadifmod', sources,
  dependencies : vapoursynth_dep,
  link_with : libs,
  install : true,
  install_dir : join_paths(vapoursynth_dep.get_pkgconfig_variable('libdir'), 'vapoursynth'),
  gnu_symbol_visibility : 'hidden'
)
