project('http_server_c', 'c')

inc = include_directories('include')

srcs = [
  'src/main.c',
  'src/client_handler.c',
  'src/sig_handler.c',
  'src/server_setup.c',
]

executable(meson.project_name(), srcs, include_directories: [inc])