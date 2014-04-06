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
         'ed8025bef58c1055de3879f469596bc5'
         '22a01b5a79dfd69cf1a522b9309cee69'
         '1a4926b726faa4ea599eaf1f06f86e9a')

prepare() {
  cd "${pkgname%%-*}-${pkgver}"
  #patch -i "${srcdir}/enable_transparency_options.diff"
  #patch -i "${srcdir}/enable_border_width_options.diff"
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
