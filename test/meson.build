progs = []

if get_option('MQTT_TEST_1')
  progs += [
    'connect',
    'underlying_timeout'
  ]
endif

if get_option('MQTT_TEST_2')
  progs += [
    'length_check',
    'utf8string_validate',
    'packet_id',
    'remaining_length',
    'message',
    'property'
  ]
endif

if get_option('MQTT_TEST_3')
  progs += [
    'sub',
    'pubsub',
    'pubsub_no_strand',
    'multi_sub'
  ]
endif

if get_option('MQTT_TEST_4')
  progs += [
    'async_pubsub_1',
    'async_pubsub_2'
  ]
endif

if get_option('MQTT_TEST_5')
  progs += [
    'resend',
    'resend_new_client',
    'resend_serialize',
    'resend_serialize_ptr_size'
  ]
endif

if get_option('MQTT_TEST_6')
  progs += [
    'offline',
    'manual_publish',
    'retain',
    'will'
  ]
endif

if get_option('MQTT_TEST_7')
  progs += [
    'as_buffer_sub',
    'as_buffer_pubsub',
    'as_buffer_async_pubsub_1',
    'as_buffer_async_pubsub_2'
  ]
endif

boost_unit_test_framework_dep = dependency(
  'boost', 
  modules : 'unit_test_framework', 
  version : '>=1.67.0'
)

foreach p : progs
  exe = executable(p.underscorify(),
    p + '.cpp', 
    include_directories : include_directories('.'),
    dependencies : [boost_unit_test_framework_dep, mqtt_cpp_dep],
    cpp_args : cpp_args
  )
  test(p.underscorify(), exe)
endforeach

#   FILE(COPY ${CMAKE_CURRENT_SOURCE_DIR}/../test/certs/mosquitto.org.crt DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
#   FILE(COPY ${CMAKE_CURRENT_SOURCE_DIR}/../test/certs/server.crt.pem DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
#   FILE(COPY ${CMAKE_CURRENT_SOURCE_DIR}/../test/certs/server.key.pem DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
#   FILE(COPY ${CMAKE_CURRENT_SOURCE_DIR}/../test/certs/cacert.pem DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
