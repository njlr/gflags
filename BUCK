# TODO: Replace wrapped CMake call
genrule(
  name = 'cmake-config', 
  out = 'out',
  srcs = glob([
    'CMakeLists.txt',
    'cmake/*',
    'src/*',
  ]),
  cmd = 'mkdir $OUT && cd $OUT && cmake $SRCDIR',
)

genrule(
  name = 'config.h', 
  out = 'config.h',
  cmd = 'cp $(location :cmake-config)/include/gflags/config.h $OUT',
)

genrule(
  name = 'gflags.h', 
  out = 'gflags.h',
  cmd = 'cp $(location :cmake-config)/include/gflags/gflags.h $OUT',
)

genrule(
  name = 'gflags_declare.h', 
  out = 'gflags_declare.h',
  cmd = 'cp $(location :cmake-config)/include/gflags/gflags_declare.h $OUT',
)

genrule(
  name = 'gflags_gflags.h', 
  out = 'gflags_gflags.h',
  cmd = 'cp $(location :cmake-config)/include/gflags/gflags_gflags.h $OUT',
)

genrule(
  name = 'gflags_completions.h', 
  out = 'gflags_completions.h',
  cmd = 'cp $(location :cmake-config)/include/gflags/gflags_completions.h $OUT',
)

cxx_library(
  name = 'gflags',
  header_namespace = '', 
  exported_headers = subdir_glob([
    ('src', '*.h'),
  ], excludes = [
    'src/windows_*.h',
  ]),
  headers = {
    'config.h': ':config.h',
    'gflags/gflags.h': ':gflags.h',
    'gflags/gflags_declare.h': ':gflags_declare.h',
    'gflags/gflags_gflags.h': ':gflags_gflags.h',
    'gflags/gflags_completions.h': ':gflags_completions.h',
  },
  platform_headers = [
    ('windows', glob([
      'src/windows_*.h',
    ])),
  ],
  srcs = glob([
    'src/*.cc',
  ], excludes = [
    'src/windows_*.cc',
  ]),
  platform_srcs = [
    ('windows', glob([
      'src/windows_*.cc',
    ])),
  ],
  visibility = [
    'PUBLIC',
  ],
)
