project('starlet-serializer', 'cpp',
  version : '1.0.0',
  meson_version : '>=1.1',
  default_options : ['cpp_std=c++20']
)

inc = include_directories('inc')

sources = files(
  'src/parser/parser.cpp',
  'src/parser/image_parser.cpp',
  'src/parser/mesh_parser.cpp',
  'src/parser/scene_parser.cpp',
  'src/parser/image/bmp_parser.cpp',
  'src/parser/image/image_parser_base.cpp',
  'src/parser/image/tga_parser.cpp',
  'src/parser/mesh/obj_parser.cpp',
  'src/parser/mesh/ply_parser.cpp',
  'src/parser/scene/camera_parser.cpp',
  'src/parser/scene/colour_parser.cpp',
  'src/parser/scene/grid_parser.cpp',
  'src/parser/scene/light_parser.cpp',
  'src/parser/scene/model_parser.cpp',
  'src/parser/scene/primitive_parser.cpp',
  'src/parser/scene/texture_parser.cpp',
  'src/parser/scene/velocity_parser.cpp',
  'src/writer/scene_writer.cpp',
)

if not get_option('build_local')
  starlet_math = subproject('starlet_math')
  starlet_math_dep = starlet_math.get_variable('starlet_math_dep')
  starlet_logger = subproject('starlet_logger')
  starlet_logger_dep = starlet_logger.get_variable('starlet_logger_dep')
else
  starlet_math_dep = dependency('starlet_math')
  starlet_logger_dep = dependency('starlet_logger')
endif

starlet_serializer_lib = static_library('starlet_serializer', sources,
  include_directories : inc,
  dependencies : [starlet_math_dep, starlet_logger_dep]
)

starlet_serializer_dep = declare_dependency(
  link_with : starlet_serializer_lib,
  include_directories : inc,
  dependencies : [starlet_math_dep, starlet_logger_dep]
)

if get_option('build_tests')
  gtest_dep = dependency('gtest_main',
    fallback : ['gtest', 'gtest_main_dep']
  )
  subdir('tests')
endif
