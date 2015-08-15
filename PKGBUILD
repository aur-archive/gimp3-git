# Maintainer: Yosef Or Boczko <yoseforb@gmail.com>

_pkgname=gimp
pkgname=gimp3-git
pkgver=1846.gb36acd5
pkgrel=1
_realver=2.9.99
pkgdesc="GNU Image Manipulation Program"
arch=('i686' 'x86_64')
url="http://www.gimp.org/"
license=('GPL' 'LGPL')
depends=('babl>=0.1.11' 'gegl>=0.3.0' 'lcms' 'libxpm' 'libwmf' 'libxmu' 'librsvg' 'libmng' 'dbus-glib'
		  'libexif' 'jasper' 'desktop-file-utils' 'hicolor-icon-theme')
makedepends=('intltool' 'libwebkit' 'poppler-glib' 'alsa-lib' 'iso-codes' 'curl' 'ghostscript' 'libxslt' 'gtk-doc')
optdepends=('gutenprint: for sophisticated printing only as gimp has built-in cups print support'
	    'libwebkit: for the help browser' 
	    'poppler-glib: for pdf support'
	    'alsa-lib: for MIDI event controller module'
	    'curl: for URI support'
	    'xorg-server-xvfb: for xvfb-run'
	    'ghostscript: for postscript support')
options=('!libtool' '!makeflags')
conflicts=('gimp-devel' 'gimp')
install=gimp3.install
replaces=('gimp')
provides=("gimp=$_realve" "gimp3=_realver")
conflicts=('gimp')
source=('git://git.gnome.org/gimp#branch=gtk3-port')
sha256sums=('SKIP')

 pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --always | sed 's/-/./g'
}

build() {
  cd "$srcdir/$_pkgname"

  # support for automake 1.14
  sed -i -e 's/automake-1.11/automake-1.14/g' \
  -e 's/aclocal-1.11/aclocal-1.14/g' autogen.sh

  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
    --enable-mp --enable-gimp-console \
    --disable-python --with-gif-compression=lzw --with-libcurl \
    --without-aa --without-gvfs \
    --enable-gtk-doc
  make
}

package() {
  cd "$srcdir/$_pkgname"
  make DESTDIR="${pkgdir}" install  
}
