progs = [
  'no_tls_client',
  'no_tls_server',
  'no_tls_both',
  'v5_no_tls_client',
  'v5_no_tls_server',
  'v5_no_tls_both',
  'v5_no_tls_prop',
  'redirect',
  'broker'
]

if get_option('MQTT_USE_TLS')
  progs += [
    'tls_client',
    'tls_server',
    'tls_both',
  ]
endif

if get_option('MQTT_USE_WS')
  progs += [
    'no_tls_ws_client',
    'no_tls_ws_server',
    'no_tls_ws_both'
  ]
endif

if get_option('MQTT_USE_WS') and get_option('MQTT_USE_TLS')
  progs += [
    'tls_ws_client',
    'tls_ws_server',
    'tls_ws_both'
  ]
endif

foreach p : progs
  exe = executable(p.underscorify(),
    p + '.cpp', 
    include_directories : include_directories('.'),
    dependencies : mqtt_cpp_dep,
    cpp_args : cpp_args
  )
  test(p.underscorify(), exe)
endforeach
