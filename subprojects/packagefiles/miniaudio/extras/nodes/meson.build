foreach node : [
  'ma_channel_combiner_node',
  'ma_channel_separator_node',
  'ma_ltrim_node',
  'ma_reverb_node',
  'ma_vocoder_node',
]
  if ma_impl_workaround
    ma_extra_srcs += files(f'@node@/@node@.c')
  else
    ma_all_libs += static_library(
      node,
      f'@node@/@node@.c',
      dependencies: ma_sys_deps,
      c_args: ma_extras_c_args,
      install: false,
      implicit_include_directories: false,
      include_directories: ma_inc,
      pic: true,
    )
  endif

  if examples.allowed() and device_io.enabled()
    executable(
      f'@node@_example',
      f'@node@/@node@_example.c',
      dependencies: ma_sys_deps,
      install: false,
      implicit_include_directories: false,
      include_directories: ma_inc,
    )
  endif
endforeach
