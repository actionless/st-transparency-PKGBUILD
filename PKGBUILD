# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Contributor: Evžen Kirillov <actionless.loveless gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st-transparency-git
appname='st'
conflicts=(${appname})
provides=(${appname})
pkgver=20140710.2690249
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X with patches for transparency and separate border width.'
arch=('i686' 'x86_64')
pkgrel=1
license=('MIT')
depends=('libxext' 'libxft')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(
	git://git.suckless.org/st
	enable_transparency_options.diff
	enable_border_width_options.diff
	config.diff
	config.diff.lcars
	config.diff.light
)
md5sums=('SKIP'
         '00604e197295823fd44a3e5b36729cf9'
         'cc7021a496ce9373432100042b96b725'
         'SKIP'
         'a46f4e8a507d2aa4e28568e72052e3a6'
         '9cd0e3e301d61c3ebc83d3472bf8a9a6')

pkgver(){
	cd "${srcdir}/${_appname}"
	git log -1 --format='%cd.%h' --date=short | tr -d -
}

prepare() {
	cd "${srcdir}/${appname}"
	cp config.def.h config.h
	for patch_file in $(ls ${srcdir}/*.diff); do
		echo "==> applying $(basename ${patch_file})"
		patch -i "$patch_file"
	done
}

build() {
	cd $srcdir/$appname
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd $srcdir/$appname
	make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
