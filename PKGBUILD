# Maintainer: xantares <xantares09 at hotmail dot com>

_pkgname=libusbx
pkgname=mingw-w64-i$_pkgname
pkgver=1.0.17
pkgrel=2
depends=('mingw-w64-crt')
makedepends=('mingw-w64-gcc' 'automake' 'autoconf' 'libtool')
pkgdesc="Library that provides generic access to USB device (mingw-w64)"
arch=(any)
url="http://libusbx.org"
license=('LGPL')
source=(http://downloads.sourceforge.net/libusbx/releases/${pkgver}/libusbx-${pkgver}.tar.bz2)
options=('!libtool' '!makeflags' '!strip' '!buildflags')
md5sums=('99467ca2cb81c19c4a172de9f30e7576')
         
_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "$srcdir/${_pkgname}-${pkgver}"
  for _arch in ${_architectures}; do
    unset LDFLAGS
    mkdir -p build-${_arch} && pushd build-${_arch}
    ../configure --prefix=/usr/${_arch} \
                 --host=${_arch} \
                 --enable-shared
    make
    popd
  done
}

package () {
  for _arch in ${_architectures}; do
    cd "$srcdir/${_pkgname}-${pkgver}/build-${_arch}"
    make install DESTDIR="$pkgdir"
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a    
  done
}
