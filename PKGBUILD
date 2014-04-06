# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st
pkgver=0.5
pkgrel=0
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxext' 'libxft')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(
	http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
	enable_transparency_options.diff
	enable_border_width_options.diff
	config.h
)
md5sums=('4f8ae2737120a8cba34b23c6020fe51e'
         'a2c0fa1d8c6eb00fe7629f58b3a78b97'
         '8cb0130be092883eb53e8514364c726b'
         'c7644d340cb9004a698b17a5bca31619')

prepare() {
  cd "${pkgname%%-*}-${pkgver}"
  patch -i "${srcdir}/enable_transparency_options.diff"
  patch -i "${srcdir}/enable_border_width_options.diff"
}

build() {
  cp ${srcdir}/config.h $srcdir/$pkgname-$pkgver/
  cd $srcdir/$pkgname-$pkgver
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
