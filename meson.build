project('radare2', 'c')
version = '1.5.0-git'

# system dependencies
cc = meson.get_compiler('c')
# required for linux
ldl = cc.find_library('dl', required: false)
pth = cc.find_library('pthread', required: false)
utl = cc.find_library('util', required: false)
mth = cc.find_library('m', required: false)

# detect OS
if cc.get_define('__linux__') == '1'
  host_os = 'linux'
else
  host_os = 'darwin'
endif

if host_machine.system() == 'windows'
  platform_deps = [cc.find_library('ws2_32')] # ,cc.find_library('capstone',dirs :'d:/2017/radare/myradare2/shlr/capstone/msvc/Release')]
  platform_librinc  = ['../include/msvc']
  platform_binrinc  = ['../../libr/include/msvc']
  host_os = 'windows'
else
  platform_librinc = []
  platform_binrinc = []
endif
subdir('libr/util')
subdir('binr/rax2')

platform_librinc = '.'
#'/usr/include'

# load plugin configuration
subdir('libr')

conf_data = configuration_data()
conf_data.set('version', version)
conf_data.set('plugins_core', '&r_core_plugin_' + ',&r_core_plugin_'.join(core) + ', 0')
conf_data.set('plugins_anal', '&r_anal_plugin_' + ',&r_anal_plugin_'.join(anal) + ', 0')
conf_data.set('plugins_asm', '&r_asm_plugin_' + ',&r_asm_plugin_'.join(asm) + ', 0')
conf_data.set('plugins_bp', '&r_bp_plugin_' + ',&r_bp_plugin_'.join(bp) + ', 0')
conf_data.set('plugins_bin', '&r_bin_plugin_' + ',&r_bin_plugin_'.join(bin) + ', 0')
conf_data.set('plugins_crypto', '&r_crypto_plugin_' + ',&r_crypto_plugin_'.join(crypto) + ', 0')
conf_data.set('plugins_io', '&r_io_plugin_' + ',&r_io_plugin_'.join(io) + ', 0')
conf_data.set('plugins_fs', '&r_fs_plugin_' + ',&r_fs_plugin_'.join(fs) + ', 0')
conf_data.set('plugins_debug', '&r_debug_plugin_' + ',&r_debug_plugin_'.join(debug) + ', 0')
conf_data.set('plugins_egg', '&r_egg_plugin_' + ',&r_egg_plugin_'.join(egg) + ', 0')
conf_data.set('plugins_lang', '&r_lang_plugin_' + ',&r_lang_plugin_'.join(lang) + ', 0')
conf_data.set('plugins_parse', '&r_parse_plugin_' + ',&r_parse_plugin_'.join(parse) + ', 0')
configure_file(input : 'libr/config.h.in',
               output : 'config.h',
               configuration : conf_data)

userconf = configuration_data()
userconf.set('PREFIX', '/usr')
userconf.set('LIBDIR', '/usr/lib')
userconf.set('INCLUDEDIR', '/usr/include')
userconf.set('DATADIR', '/usr/share')
userconf.set('HAVE_LIB_MAGIC', 0)
userconf.set('USE_LIB_MAGIC', 0)
userconf.set('HAVE_OPENSSL', 0)
userconf.set('HAVE_FORK', 1)
userconf.set('WITH_GPL', 1)
userconf.set('DEBUGGER', 1)
configure_file(input : 'libr/include/r_userconf.h.in',
               output : 'r_userconf.h',
               configuration : userconf)

subdir('libr/hash')
subdir('libr/crypto')
subdir('libr/socket')
subdir('libr/io')
subdir('binr/rahash2')
subdir('binr/rarun2')

subdir('libr/bp')
subdir('libr/syscall')
subdir('libr/cons')
subdir('libr/search')
subdir('libr/magic')

subdir('libr/flag')
subdir('libr/reg')

subdir('libr/bin')
subdir('libr/config')

subdir('libr/parse')
subdir('libr/lang')

subdir('libr/asm')
subdir('libr/anal')
subdir('binr/rasm2')
subdir('libr/egg')

subdir('libr/fs')

subdir('libr/debug')

subdir('libr/core')

subdir('binr/rabin2')
subdir('binr/radare2')
subdir('binr/ragg2')
