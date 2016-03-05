# Copyright (c) 2015 Nuxi, https://nuxi.nl/
#
# This file is distributed under a 2-clause BSD license.
# See the LICENSE file for details.

import os

def build(ctx):
    srcdir = ctx.extract('Python-%(version)s')

    # First build a native binary, this will be used by the cross-build
    # to generate some files (see also patch-makefile-regen)
    hostbuild = srcdir.host().autoconf()
    hostbuild.make()

    build = srcdir.autoconf([
        '--build=x86_64-unknown-freebsd',
        'ac_cv_buggy_getaddrinfo=no',
        'ac_cv_file__dev_ptc=no',
        'ac_cv_file__dev_ptmx=no',
        'ac_cv_have_long_long_format=yes',
        'PYTHON_FOR_BUILD=%s' % os.path.join(str(hostbuild), 'python'),
    ])
    with srcdir.diff('/home/edje/python.diff'):
        build.debug_shell()

    build.make()
    build.make_install().install()

package(
    name='python',
    version='3.5.1',
    homepage='https://www.python.org/',
    maintainer='info@nuxi.nl',
    lib_depends={'c-runtime'},
    build_cmd=build,
)

distfile(
    name='Python-3.5.1.tar.xz',
    checksum='c6d57c0c366d9060ab6c0cdf889ebf3d92711d466cc0119c441dbf2746f725c9',
    master_sites={'https://www.python.org/ftp/python/3.5.1/'},
    unsafe_string_sources={
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
