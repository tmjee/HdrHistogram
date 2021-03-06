# SConstruct
# Written by Michael Barker and released to the public domain,
# as explained at http://creativecommons.org/publicdomain/zero/1.0/

import os

version = '1.0.9'
version_directory = 'target/c/hdr_histogram-' + version
lib_directory     = version_directory + '/lib/'
bin_directory     = version_directory + '/bin/'
src_directory     = version_directory + '/src/'
test_directory    = version_directory + '/test/'
include_directory = version_directory + '/include/'

env = Environment()
env['ENV']['PATH'] = os.environ['PATH']
env['CC']  = 'clang'
env['CPPPATH'] = []
env['CPPFLAGS'] = ['-g', '-Wall']
env['TARFLAGS'] = ['-c', '-z']
env['TARSUFFIX'] = ['.tar.gz']

bin = env.Clone()
bin['CPPDEFINES'] = ['__LZCNT__']
library = bin.StaticLibrary(lib_directory + 'hdr_histogram', Glob('src/main/c/*.c'))

tst = env.Clone()
tst['CPPPATH'] = ['src/main/c']
tst['LIBS'] = ['hdr_histogram']
tst['LIBPATH'] = [lib_directory]
tst['LINKFLAGS'] = ['-lm']
tst.Program(bin_directory + 'alltests', Glob('src/test/c/*.c'))

exp = env.Clone()
exp['CPPPATH'] = ['src/main/c']
exp['LIBS'] = ['hdr_histogram']
exp['LIBPATH'] = [lib_directory]
exp['LINKFLAGS'] = ['-lm']
exp.Program(bin_directory + 'format_example', ['src/examples/c/hdr_histogram_format_example.c'])

env.Install(include_directory, Glob('src/main/c/*.h'))
env.Install(src_directory, Glob('src/main/c/*.c') + Glob('src/main/c/*.h'))
env.Install(test_directory, Glob('src/test/c/*.c') + Glob('src/test/c/*.h'))

env.Tar('target/c/hdr_histogram-' + version, Dir('hdr_histogram-' + version),
        TARFLAGS = ['-c', '-z', '-Ctarget/c'])
