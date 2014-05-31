# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Contributor: Evžen Kirillov <actionless.loveless gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st-transparency-git
appname='st'
conflicts=(${appname})
provides=(${appname})
pkgver=20140528.12e84eb
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X with patches for transparency and separate border width.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxext' 'libxft')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(
	git://git.suckless.org/st
	enable_transparency_options.diff
	enable_border_width_options.diff
	config.h
)
md5sums=('SKIP'
         '44ba565b9a4fe97d79d73be903a84054'
         '1bd6ecfac11ac54f520e9c1184fb143c'
         '5f322ee62c0bd72e990648e3ff6ab7d2')

pkgver(){
	cd "${srcdir}/${_appname}"
	git log -1 --format='%cd.%h' --date=short | tr -d -
}

prepare() {
	cd "${srcdir}/${appname}"
	for patch_file in $(ls ${srcdir}/*.diff); do
		echo "applying ${patch_file}"
		patch -i "$patch_file"
	done
}

build() {
	cp ${srcdir}/config.h $srcdir/$appname/
	cd $srcdir/$appname
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd $srcdir/$appname
	make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
