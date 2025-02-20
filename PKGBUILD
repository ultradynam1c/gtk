# Maintainer: Connor Behan <connor.behan@gmail.com>
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=gtk
pkgver=1.2.10
pkgrel=19
pkgdesc="A multi-platform toolkit (v1)"
arch=('i686' 'x86_64' 'aarch64')
url="http://www.gtk.org/"
license=('LGPL')
depends=('libxi' 'glib')
makedepends=('libxt')
source=(https://download.gnome.org/sources/gtk+/1.2/gtk+-${pkgver}.tar.gz
        aclocal-fixes.patch)
sha1sums=('a5adcb909257da01ae4d4761e1d41081d06e4d7c'
          'b034e33efb85d27f3f3fb082c404e3b6ea79259f')

prepare() {
  cd gtk+-${pkgver}
  cp /usr/share/libtool/build-aux/config.guess .
  cp /usr/share/libtool/build-aux/config.sub .
  patch -p0 -i "${srcdir}/aclocal-fixes.patch"
  sed -i "/ac_cpp=/s/\$CPPFLAGS/\$CPPFLAGS -O2/" configure
  sed -i -e "s|&name|(char \*\*)\&name|" gdk/gdkwindow.c
}

build() {
  cd gtk+-${pkgver}
  CFLAGS="-Wno-format-security -Wno-implicit-int -include stdio.h -include stdlib.h -include string.h" ./configure --prefix=/usr --sysconfdir=/etc \
    --mandir=/usr/share/man --infodir=/usr/share/info \
    --with-xinput=xfree
  make
}

package() {
  cd gtk+-${pkgver}
  make DESTDIR="${pkgdir}" install
}
