all_tests = [
  '232c93d07b74.c',
  '35fa71a030ca.c',
  '500f9fbadef8.c',
  '7ad0e4b2f83c.c',
  '8a9973408177.c',
  '917257daa0fe.c',
  'a0908ae19763.c',
  'a4c0b3decb33.c',
  'accept.c',
  'accept-link.c',
  'accept-reuse.c',
  'accept-test.c',
  'across-fork.c',
  'b19062a56726.c',
  'b5837bd5311d.c',
  'buf-ring.c',
  'ce593a6c480a.c',
  'close-opath.c',
  'connect.c',
  'connect-rep.c',
  'coredump.c',
  'cq-full.c',
  'cq-overflow.c',
  'cq-peek-batch.c',
  'cq-ready.c',
  'cq-size.c',
  'd4ae271dfaae.c',
  'd77a67ed5f27.c',
  'defer.c',
  'defer-taskrun.c',
  'double-poll-crash.c',
  'drop-submit.c',
  'eeed8b54e0df.c',
  'empty-eownerdead.c',
  'eploop.c',
  'eventfd.c',
  'eventfd-disable.c',
  'eventfd-reg.c',
  'eventfd-ring.c',
  'evloop.c',
  'exec-target.c',
  'exit-no-cleanup.c',
  'fadvise.c',
  'fallocate.c',
  'fc2a85cb02ef.c',
  'fd-pass.c',
  'file-register.c',
  'files-exit-hang-poll.c',
  'files-exit-hang-timeout.c',
  'file-update.c',
  'file-verify.c',
  'fixed-buf-iter.c',
  'fixed-link.c',
  'fixed-reuse.c',
  'fpos.c',
  'fsnotify.c',
  'fsync.c',
  'hardlink.c',
  'io-cancel.c',
  'iopoll.c',
  'iopoll-leak.c',
  'iopoll-overflow.c',
  'io_uring_enter.c',
  'io_uring_passthrough.c',
  'io_uring_register.c',
  'io_uring_setup.c',
  'lfs-openat.c',
  'lfs-openat-write.c',
  'link.c',
  'link_drain.c',
  'link-timeout.c',
  'madvise.c',
  'mkdir.c',
  'msg-ring.c',
  'msg-ring-flags.c',
  'msg-ring-overflow.c',
  'multicqes_drain.c',
  'no-mmap-inval.c',
  'nolibc.c',
  'nop-all-sizes.c',
  'nop.c',
  'openat2.c',
  'open-close.c',
  'open-direct-link.c',
  'open-direct-pick.c',
  'personality.c',
  'pipe-bug.c',
  'pipe-eof.c',
  'pipe-reuse.c',
  'poll.c',
  'poll-cancel.c',
  'poll-cancel-all.c',
  'poll-cancel-ton.c',
  'poll-link.c',
  'poll-many.c',
  'poll-mshot-overflow.c',
  'poll-mshot-update.c',
  'poll-race.c',
  'poll-race-mshot.c',
  'poll-ring.c',
  'poll-v-poll.c',
  'pollfree.c',
  'probe.c',
  'read-before-exit.c',
  'read-write.c',
  'recv-msgall.c',
  'recv-msgall-stream.c',
  'recv-multishot.c',
  'reg-fd-only.c',
  'reg-hint.c',
  'reg-reg-ring.c',
  'regbuf-merge.c',
  'register-restrictions.c',
  'rename.c',
  'ringbuf-read.c',
  'ring-leak2.c',
  'ring-leak.c',
  'rsrc_tags.c',
  'rw_merge_test.c',
  'self.c',
  'send_recv.c',
  'send_recvmsg.c',
  'send-zerocopy.c',
  'shared-wq.c',
  'short-read.c',
  'shutdown.c',
  'sigfd-deadlock.c',
  'single-issuer.c',
  'skip-cqe.c',
  'socket.c',
  'socket-io-cmd.c',
  'socket-rw.c',
  'socket-rw-eagain.c',
  'socket-rw-offset.c',
  'splice.c',
  'sq-full.c',
  'sqpoll-cancel-hang.c',
  'sqpoll-disable-exit.c',
  'sq-poll-dup.c',
  'sqpoll-exit-hang.c',
  'sq-poll-kthread.c',
  'sq-poll-share.c',
  'sqpoll-sleep.c',
  'sq-space_left.c',
  'stdout.c',
  'submit-and-wait.c',
  'submit-link-fail.c',
  'submit-reuse.c',
  'symlink.c',
  'sync-cancel.c',
  'teardowns.c',
  'thread-exit.c',
  'timeout.c',
  'timeout-new.c',
  'tty-write-dpoll.c',
  'unlink.c',
  'version.c',
  'wakeup-hang.c',
  'wq-aff.c',
  'xattr.c',
]

if has_statx or glibc_statx
  all_tests += ['statx.c']
endif

if has_cxx
  all_tests += ['sq-full-cpp.cc']
endif

runtests_sh = find_program('runtests.sh')
runtests_loop_sh = find_program('runtests-loop.sh')
runtests_quiet_sh = find_program('runtests-quiet.sh')

xcflags = ['-Wno-sign-compare']
if has_stringop_overflow
  xcflags = xcflags + ['-Wstringop-overflow=0']
endif
if has_array_bounds
  xcflags = xcflags + ['-Warray-bounds=0']
endif

fs = import('fs')

foreach test_source : all_tests
  test_name = fs.stem(test_source)
  executable(
    test_name,
    [test_source, 'helpers.c'],
    c_args: xcflags,
    cpp_args: xcflags,
    include_directories: inc,
    link_with: liburing.get_static_lib(),
    dependencies: [thread_dep],
    install: true,
    install_dir: get_option('datadir') / 'liburing-test',
  )

  test(
    test_name,
    runtests_sh,
    args: test_name,
    is_parallel: false,
    workdir: meson.current_build_dir(),
    suite: 'once',
  )

  test(
    test_name + '_loop',
    runtests_loop_sh,
    args: test_name,
    is_parallel: false,
    workdir: meson.current_build_dir(),
    suite: 'loop',
  )

  test(
    test_name + '_quiet',
    runtests_quiet_sh,
    args: test_name,
    workdir: meson.current_build_dir(),
    suite: 'parallel',
  )
endforeach

add_test_setup(
  'runtests',
  exclude_suites: ['loop', 'parallel'],
  is_default: true,
)

configure_file(
  input: 'runtests.sh',
  output: 'runtests.sh',
  copy: true,
)

configure_file(
  input: 'runtests-loop.sh',
  output: 'runtests-loop.sh',
  copy: true,
)

configure_file(
  input: 'config',
  output: 'config.local',
  copy: true,
)

install_data(
  'runtests.sh',
  'runtests-loop.sh',
  install_dir: get_option('datadir') / 'liburing-test',
)
