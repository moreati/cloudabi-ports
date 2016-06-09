# Copyright (c) 2015 Nuxi, https://nuxi.nl/
#
# This file is distributed under a 2-clause BSD license.
# See the LICENSE file for details.

import os

def build(ctx):
    srcdir = ctx.extract('cpython-d1f2fdde1a305911a04bbdc0558cddfadb3ffb39')

    # First build a native binary, this will be used by the cross-build
    # to generate some files (see also patch-makefile-regen)
    hostbuild = srcdir.host().autoconf()
    hostbuild.make()

    build = srcdir.autoconf([
        '--build=x86_64-unknown-freebsd',
        '--disable-shared',
        '--without-ensurepip',
        'ac_cv_buggy_getaddrinfo=no',
        'ac_cv_file__dev_ptc=no',
        'ac_cv_file__dev_ptmx=no',
        'ac_cv_have_long_long_format=yes',
        'ac_cv_posix_semaphores_enabled=no',
        'CPPFLAGS=-static',
        'LDFLAGS=-static -static-libgcc',
        'PYTHON_FOR_BUILD=_PYTHON_PROJECT_BASE=$(abs_builddir) '
                         '_PYTHON_HOST_PLATFORM=$(_PYTHON_HOST_PLATFORM) '
                         'PYTHONPATH=$(shell test -f pybuilddir.txt '
                                            '&& echo $(abs_builddir)/`cat pybuilddir.txt`:)'
                                    '$(srcdir)/Lib:'
                                    '$(srcdir)/Lib/$(PLATDIR) '
                         '%s' % os.path.join(str(hostbuild), 'python'),
    ])
    with srcdir.diff('/home/edje/python.diff'):
        build.debug_shell()

    build.make([
        '--assume-new=Parser/pgen',
        '--assume-new=Programs/_freeze_importlib',
    ])
    install = build.make_install()
    install.install()

package(
    name='python',
    version='3.6.0',
    homepage='https://www.python.org/',
    maintainer='info@nuxi.nl',
    lib_depends={'c-runtime'},
    build_cmd=build,
)

distfile(
    name='cpython-d1f2fdde1a305911a04bbdc0558cddfadb3ffb39.zip',
    checksum='2e333d169defd4612bc69525fbd1292e72c675cc08f3d896e91f31d988084ab0',
    master_sites={'https://github.com/python/cpython/archive/'},
    unsafe_string_sources={
        'Modules/_ctypes/_ctypes.c',
        'Modules/_ctypes/_ctypes_test.c',
        'Modules/_datetimemodule.c',
        'Modules/_decimal/_decimal.c',
        'Modules/_decimal/libmpdec/io.c',
        'Modules/_elementtree.c',
        'Modules/_multiprocessing/semaphore.c',
        'Modules/_testbuffer.c',
        'Modules/_testcapimodule.c',
        'Modules/cjkcodecs/cjkcodecs.h',
        'Modules/getpath.c',
        'Modules/main.c',
        'Modules/posixmodule.c',
        'Modules/pyexpat.c',
        'Modules/unicodedata.c',
        'Objects/bytesobject.c',
        'Objects/memoryobject.c',
        'Objects/structseq.c',
        'Objects/typeobject.c',
        'Objects/unicodeobject.c',
        'Parser/parsetok.c',
        'Parser/tokenizer.c',
        'Python/ast.c',
        'Python/codecs.c',
        'Python/pystrtod.c',
        'Python/traceback.c',
    },
)
