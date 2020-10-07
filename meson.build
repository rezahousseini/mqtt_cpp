project('mqtt_cpp', 'cpp', 
  license: 'BSL-1.0',
  default_options : ['warning_level=0', 'cpp_std=c++14']
)

if get_option('MQTT_STD_VARIANT') or \
   get_option('MQTT_STD_OPTIONAL') or \
   get_option('MQTT_STD_ANY') or \
   get_option('MQTT_STD_STRING_VIEW') or \
   get_option('MQTT_STD_SHARED_PTR_ARRAY')
  cpp_args = ['std=c++17']
else
  cpp_args = []
endif

thread_dep = dependency('threads')

if meson.is_cross_build()
  cxx = meson.get_compiler('cpp')
  boost_system_lib = cxx.find_library('boost_system', 
    dirs : meson.get_cross_property('boost_librarydir')
  )
  boost_date_time_lib = cxx.find_library('boost_date_time', 
    dirs : meson.get_cross_property('boost_librarydir')
  )
  boost_inc = include_directories(meson.get_cross_property('boost_includedir'))
  boost_dep = declare_dependency(include_directories : boost_inc, 
    dependencies : [boost_system_lib, boost_date_time_lib]
  )
else
  boost_dep = dependency('boost', 
    version : '>=1.67.0'
  )
endif

openssl_dep = dependency('openssl', required : get_option('MQTT_USE_TLS'))

mqtt_cpp_dep = declare_dependency(
  include_directories: include_directories('include'),
  dependencies : [thread_dep, boost_dep, openssl_dep],
  compile_args : ['-DBOOST_ASIO_USE_TS_EXECUTOR_AS_DEFAULT'],
)

if not meson.is_subproject()
  install_subdir(
    'include', 
    install_dir: 'include', 
    strip_directory : true,
    exclude_files : 'CMakeLists.txt'
  )
  
  pkgc = import('pkgconfig')
  pkgc.generate(
    name: 'mqtt_cpp',
    version: meson.project_version(),
    description: 'MQTT client/server for C++14 based on Boost.Asio'
  )
endif

if get_option('MQTT_BUILD_TESTS')
  subdir('test')
endif

if get_option('MQTT_BUILD_EXAMPLES')
  subdir('example')
endif
