# Copyright (c) 2015-2016 Nuxi, https://nuxi.nl/
#
# This file is distributed under a 2-clause BSD license.
# See the LICENSE file for details.


def build(ctx):
    build = ctx.extract().gnu_configure()
    build.make(['buildlib'])
    build.make_install(['installlib']).install()

package(
    name='expat',
    version='2.2.0',
    homepage='http://expat.sourceforge.net/',
    maintainer='info@nuxi.nl',
    lib_depends={'c-runtime'},
    build_cmd=build,
)

distfile(
    name='expat-2.2.0.tar.bz2',
    checksum='d9e50ff2d19b3538bd2127902a89987474e1a4db8e43a66a4d1a712ab9a504ff',
    master_sites=sites_sourceforge('expat/expat/2.2.0'),
)
