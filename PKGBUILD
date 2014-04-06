# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st
pkgver=0.4.1
pkgrel=1
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
md5sums=(
	'fa03d702b6d67de395975155c87084e9'
	'SKIP'
	'SKIP'
	'SKIP'
)

prepare() {
  cd "${pkgname%%-*}-${pkgver}"
  ls -la
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
