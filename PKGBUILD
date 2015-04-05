

# Maintainer: Benjamin Hedrich <kiwisauce (a) pagenotfound (dot) de>
# Based on package hts-tvheadend-svn by azleifel <azleifel at googlemail dot com>

pkgname=tvheadend-git-joschi127
_gitname='tvheadend'
#pkgver=3.4fixed
#pkgver=3.9fixed
pkgver=3.9master
pkgrel=1
pkgdesc="TV streaming server for Linux"
arch=('i686' 'x86_64')
url="https://tvheadend.org/"
license=('GPL3')
depends=('avahi' 'openssl' 'python2')
makedepends=('git')
optdepends=(
	'xmltv: For an alternative source of programme listings'
	'ffmpeg-compat: for transcoding support')
provides=('tvheadend')
conflicts=('tvheadend' 'hts-tvheadend' 'hts-tvheadend-svn')
install=tvheadend.install

source=("git+https://github.com/tvheadend/tvheadend.git#commit=e4f034aed3ec1fda9439e741e8690a839b5b68ea"
        #"git+https://github.com/tvheadend/tvheadend.git#tag=v3.9"
        #"git+https://github.com/joschi127/tvheadend.git#branch=joschi127/3.4fixed"
        #"git+https://github.com/joschi127/tvheadend.git#branch=joschi127/3.9fixed"
	'tvheadend.service')

md5sums=('SKIP'
         'b546f4486f0d28bea13ad1fb676acb27')

#pkgver() {
#	cd ${_gitname}
#	echo $(git rev-list --count HEAD)+g$(git rev-parse --short HEAD)
#}

build() {
	cd ${_gitname}
	if [ -d "/usr/include/ffmpeg-compat" ]; then
		export PKG_CONFIG_PATH=/usr/lib/ffmpeg-compat/pkgconfig:$PKG_CONFIG_PATH
		CFLAGS+=" `pkg-config --cflags libavcodec libavutil libavformat libswscale` "
		LDFLAGS+=" `pkg-config --libs libavcodec libavutil libavformat libswscale` -Wl,-rpath /usr/lib/ffmpeg-compat"
	fi
	./configure --prefix=/usr --mandir=/usr/share/man/man1 --python=python2 --release
	make
}

package() {
	cd ${_gitname}
	make DESTDIR="$pkgdir/" install
	install -D -m 644 "$srcdir/tvheadend.service" "$pkgdir/usr/lib/systemd/system/tvheadend.service"
}


