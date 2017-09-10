project('libcpr', 'cpp',default_options : ['cpp_std=c++14'])


inc = include_directories('include')

libcurl = dependency('libcurl')

cpr_sources = [
  'cpr/auth.cpp',
  'cpr/cookies.cpp',
  'cpr/cprtypes.cpp',
  'cpr/digest.cpp',
  'cpr/error.cpp',
  'cpr/multipart.cpp',
  'cpr/parameters.cpp',
  'cpr/payload.cpp',
  'cpr/proxies.cpp',
  'cpr/session.cpp',
  'cpr/ssl_options.cpp',
  'cpr/timeout.cpp',
  'cpr/util.cpp'
]

cpr_lib = library('cpr',
                       cpr_sources,
                       include_directories : inc,
                       dependencies : libcurl,
                       install : true
                       )


cpr = declare_dependency(link_with : cpr_lib,
                                dependencies : libcurl,
                                include_directories : inc)

gtest_dep = dependency('gtest', required : true, main : false, fallback:['gtest','gtest_mainless_dep'])
mongoose_dep = dependency('mongoose', required : true, fallback:['mongoose','mongoose'])


tests = [
  'get',
  'post',
  'session',
  'async',
  'proxy',
  'head',
  'delete',
  'put',
  'callback',
  'raw_body',
  'options',
  'patch',
  'error',
  'alternating',
  'util'
]


foreach test : tests
  test_inc = include_directories('test')
  test_src = ['test/@0@_tests.cpp'.format(test), 'test/server.cpp']
  test_exe = executable(test,test_src ,
                          include_directories : test_inc,
                          dependencies : [cpr, gtest_dep, mongoose_dep])
  test(test, test_exe)
endforeach
