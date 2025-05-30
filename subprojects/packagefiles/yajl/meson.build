project(
  'YetAnotherJSONParser',
  'c',
  license: 'ISC',
  version: '2.1.0',
  meson_version: '>=0.47.0',
)

if get_option('default_library') != 'static'
  add_project_arguments(
    '-DYAJL_SHARED',
    '-DYAJL_BUILD',
    language: 'c',
  )
endif

version = configuration_data()
version.set('YAJL_MAJOR', 2)
version.set('YAJL_MINOR', 1)
version.set('YAJL_MICRO', 0)
api = files(
  'src/api/yajl_common.h',
  'src/api/yajl_gen.h',
  'src/api/yajl_parse.h',
  'src/api/yajl_tree.h',
)
versionh = files('src/api/yajl_version.h.cmake')
subdir('include-workaround-meson/yajl')
src = files(
  'src/yajl.c',
  'src/yajl_alloc.c',
  'src/yajl_alloc.h',
  'src/yajl_buf.c',
  'src/yajl_buf.h',
  'src/yajl_bytestack.h',
  'src/yajl_encode.c',
  'src/yajl_encode.h',
  'src/yajl_gen.c',
  'src/yajl_lex.c',
  'src/yajl_lex.h',
  'src/yajl_parser.c',
  'src/yajl_parser.h',
  'src/yajl_tree.c',
  'src/yajl_version.c',
)
yajl = library(
  'yajl',
  src,
  include_directories: include_directories('include-workaround-meson'),
  install: true,
)
yajl_dep = declare_dependency(
  link_with: yajl,
  include_directories: include_directories('include-workaround-meson'),
)
pconf = import('pkgconfig')
pconf.generate(
  libraries: yajl,
  subdirs: 'yajl',
  version: meson.project_version(),
  name: 'Yet Another JSON Library',
  filebase: 'yajl',
  description: 'A Portable JSON parsing and serialization library in ANSI C',
)
