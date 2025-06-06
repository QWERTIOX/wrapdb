# Meson file for libccp4c (CCP4 core libraries, C part only)
project(
  'libccp4c',
  'c',
  version: '8.0.0',
  meson_version: '>=0.49.0',
  license: 'LGPL-3.0-or-later',
)

cc = meson.get_compiler('c')
mdep = cc.find_library(
  'm',
  required: false,
)

# Note that the source code assumes that datadir='share'.
# If it is not, programs using the library will not be able
# to find 'environ.def'.
datadir = get_option('datadir') / 'ccp4'

add_project_arguments(
  '-DPACKAGE_ROOT="@0@"'.format(get_option('prefix')),
  language: 'c',
)
add_project_arguments(
  cc.get_supported_arguments(
    '-Wno-uninitialized',
    '-Wno-unused-function',
    '-Wno-stringop-truncation',
    '-Wno-stringop-overflow',
    '-Wno-format-overflow',
    '-Wno-misleading-indentation',
    '-Wno-pointer-compare',
  ),
  language: 'c',
)

# C library
libccp4c = library(
  'ccp4c',
  'ccp4/ccp4_array.c',
  'ccp4/cmap_accessor.c',
  'ccp4/cmap_open.c',
  'ccp4/csymlib.c',
  'ccp4/pack_c.c',
  'ccp4/ccp4_general.c',
  'ccp4/cmap_close.c',
  'ccp4/cmap_skew.c',
  'ccp4/cvecmat.c',
  'ccp4/ccp4_parser.c',
  'ccp4/cmap_data.c',
  'ccp4/cmap_stats.c',
  'ccp4/library_err.c',
  'ccp4/ccp4_program.c',
  'ccp4/cmap_header.c',
  'ccp4/cmap_symop.c',
  'ccp4/library_file.c',
  'ccp4/ccp4_unitcell.c',
  'ccp4/cmap_labels.c',
  'ccp4/cmtzlib.c',
  'ccp4/library_utils.c',
  dependencies: mdep,
  install: true,
)

# CCP4 headers are included with prefix: <ccp4/header.h>
incdir = include_directories('.')

install_headers(
  'ccp4/ccp4_file_err.h',
  'ccp4/ccp4_program.h',
  'ccp4/ccp4_unitcell.h',
  'ccp4/cmap_errno.h',
  'ccp4/cmap_stats.h',
  'ccp4/csymlib.h',
  'ccp4/library_file.h',
  'ccp4/ccp4_fortran.h',
  'ccp4/ccp4_spg.h',
  'ccp4/ccp4_utils.h',
  'ccp4/cmap_header.h',
  'ccp4/cmaplib.h',
  'ccp4/cvecmat.h',
  'ccp4/mtzdata.h',
  'ccp4/ccp4_array.h',
  'ccp4/ccp4_general.h',
  'ccp4/ccp4_sysdep.h',
  'ccp4/ccp4_vars.h',
  'ccp4/cmap_labels.h',
  'ccp4/cmaplib_f.h',
  'ccp4/overview.h',
  'ccp4/ccp4_errno.h',
  'ccp4/ccp4_parser.h',
  'ccp4/ccp4_types.h',
  'ccp4/cmap_data.h',
  'ccp4/cmap_skew.h',
  'ccp4/cmtzlib.h',
  'ccp4/pack_c.h',
  subdir: 'ccp4',
)

# Data files
install_data(
  'data/atomsf_electron.lib',
  'data/atomsf.lib',
  'data/atomsf_neutron.lib',
  'data/syminfo.lib',
  'data/symop.lib',
  install_dir: datadir,
)

# pkg-config file
pkg = import('pkgconfig')
pkg.generate(
  libccp4c,
  filebase: 'libccp4c',
  description: 'CCP4 core C libraries',
)

libccp4c_dep = declare_dependency(
  include_directories: incdir,
  link_with: libccp4c,
)
