# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgver=0.4.1
pkgname=st-transparency-git
appname='st'
conflicts=(${appname})
provides=(${appname})
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxext' 'libxft')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(
	http://dl.suckless.org/st/$appname-$pkgver.tar.gz
	http://st.suckless.org/patches/$appname-$pkgver-argbbg.diff
	enable_border_width_options.diff
	config.h
)
md5sums=('fa03d702b6d67de395975155c87084e9'
         '08ad80a8f56293bd0127db3ec25d1025'
         '8cb0130be092883eb53e8514364c726b'
         'c7644d340cb9004a698b17a5bca31619')

prepare() {
  cd "${appname}-${pkgver}"
  patch -i "${srcdir}/${appname}-${pkgver}-argbbg.diff"
  patch -i "${srcdir}/enable_border_width_options.diff"
}

build() {
  cp ${srcdir}/config.h $srcdir/$appname-$pkgver/
  cd $srcdir/$appname-$pkgver
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$appname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
