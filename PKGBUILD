# $Id$
# Maintainer: Giovanni Scafora <giovanni@archlinux.org>
# Contributor: lucke <lucke at o2 dot pl>

_pkgname=weechat
pkgname=seventy
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
provides=('weechat')
conflicts=('weechat')
source=("https://www.weechat.org/files/src/${_pkgname}-${pkgver}.tar.bz2"
        'ascii-logo.patch')
md5sums=('37c0388e5cb82fd3c3d1a533a5a5695d'
         '154df5e85037ddefcd9ae525ac2f96ca')

prepare() {
  cd ${_pkgname}-${pkgver}
  patch -Np1 -i "${srcdir}/ascii-logo.patch"

  grep -rl 'weechat' . | xargs -r -L 1 sed -i 's/weechat/seventy/g'
  grep -rl 'WeeChat' . | xargs -r -L 1 sed -i 's/WeeChat/Seventy/g'
  grep -rl 'Weechat' . | xargs -r -L 1 sed -i 's/Weechat/Seventy/g'
  grep -rl 'WEECHAT' . | xargs -r -L 1 sed -i 's/WEECHAT/SEVENTY/g'

  find . -depth -name "*weechat*" \
       -exec bash -c 'for f; do base=${f##*/}; mv -- "$f" "${f%/*}/${base//weechat/seventy}"; done' _ {} +

  cd ..
  mkdir build
}

build() {
  cd build

  cmake -Wno-dev ../${_pkgname}-${pkgver} \
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
