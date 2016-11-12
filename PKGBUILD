# $Id$
# Maintainer: Giovanni Scafora <giovanni@archlinux.org>
# Contributor: lucke <lucke at o2 dot pl>

pkgname=weechat
pkgver=1.6
pkgrel=1
pkgdesc="Fast, light and extensible IRC client (curses UI)"
arch=('i686' 'x86_64')
url="http://www.weechat.org/"
license=('GPL')
depends=('gnutls' 'curl' 'libgcrypt')
makedepends=('asciidoc' 'source-highlight' 'cmake' 'pkg-config' 'perl' 'python2'
             'lua' 'tcl' 'ruby' 'aspell' 'guile')
optdepends=('perl' 'python2' 'lua' 'tcl' 'ruby' 'aspell' 'guile')
validpgpkeys=('A9AB5AB778FA5C3522FD0378F82F4B16DEC408F8') # WeeChat (signing key)
source=(https://www.weechat.org/files/src/${pkgname}-${pkgver}.tar.bz2{,.asc})
md5sums=('37c0388e5cb82fd3c3d1a533a5a5695d'
         'SKIP')

prepare() {
  mkdir build
}

build() {
  cd build

  cmake -Wno-dev ../${pkgname}-${pkgver} \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DENABLE_MAN=ON \
        -DENABLE_DOC=ON

  make
}

package() {
  cd build

  make DESTDIR="${pkgdir}/" install
}
