# Copyright (c) 2015-2016 Nuxi, https://nuxi.nl/
#
# This file is distributed under a 2-clause BSD license.
# See the LICENSE file for details.


def build(ctx):
    root = ctx.extract('%(name)s-%(version)s.src')
    ctx.extract('libcxxabi-%(version)s.src').rename(root.path('libcxxabi'))

    # Build libc++.a.
    sources = {
        'algorithm.cpp', 'any.cpp', 'bind.cpp', 'chrono.cpp',
        'condition_variable.cpp', 'debug.cpp', 'exception.cpp',
        'future.cpp', 'hash.cpp', 'ios.cpp', 'iostream.cpp', 'locale.cpp',
        'memory.cpp', 'mutex.cpp', 'new.cpp', 'optional.cpp',
        'random.cpp', 'regex.cpp', 'shared_mutex.cpp', 'stdexcept.cpp',
        'string.cpp', 'strstream.cpp', 'system_error.cpp', 'thread.cpp',
        'typeinfo.cpp', 'utility.cpp', 'valarray.cpp'
    }
    srcdir = root.path('src')
    libcxx = ctx.archive(
        srcdir.path(f).compile(
            ['-I../include', '-I../libcxxabi/include', '-std=c++11',
             '-D_LIBCPP_BUILD_STATIC', '-DLIBCXX_BUILDING_LIBCXXABI'])
        for f in sources)
    libcxx.install('lib/libc++.a')

    # Install header files.
    headers = root.path('include')
    headers.path('CMakeLists.txt').remove()
    headers.path('support').remove()
    headers.install('include/c++/v1')

package(
    name='libcxx',
    version='3.8.0',
    homepage='http://libcxx.llvm.org/',
    maintainer='info@nuxi.nl',
    lib_depends={'c-runtime'},
    build_cmd=build,
)

distfile(
    name='libcxx-3.8.0.src.tar.xz',
    checksum='36804511b940bc8a7cefc7cb391a6b28f5e3f53f6372965642020db91174237b',
    master_sites={'http://llvm.org/releases/3.8.0/'},
)
