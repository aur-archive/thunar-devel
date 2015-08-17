# Maintainer:  cuihao <cuihao dot leo at gmail dot com>
# Contributor: Xavier Devlamynck <magicrhesus@ouranos.be>

# Original PKGBUILD (extra/thunar):
# $Id: PKGBUILD 172898 2012-12-06 12:48:55Z foutrelis $
# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Andrew Simmons <andrew.simmons@gmail.com>

pkgname=thunar-devel
_pkgname=thunar
pkgver=1.6.0
pkgrel=3
pkgdesc="Modern file manager for Xfce"
arch=('i686' 'x86_64')
url="http://thunar.xfce.org"
license=('GPL2' 'LGPL2.1')
groups=('xfce4')
depends=('desktop-file-utils' 'libexif' 'hicolor-icon-theme' 'libnotify'
         'udev' 'gtk2' 'exo>=0.10.0' 'libxfce4util' 'libxfce4ui' 'libpng')
makedepends=('intltool' 'gtk-doc' 'xfce4-panel')
optdepends=('gvfs: for trash support, mounting with udisk and remote filesystems'
            'polkit-gnome: for mounting internal partitions (needs root password)'
            'xfce4-panel: for trash applet'
            'tumbler: for thumbnail previews'
            'thunar-volman: manages removable devices'
            'thunar-archive-plugin: create and deflate archives'
            'thunar-media-tags-plugin: view/edit id3/ogg tags')
options=('!libtool')
install=$_pkgname.install
source=(http://archive.xfce.org/src/xfce/$_pkgname/1.6/Thunar-$pkgver.tar.bz2
        thunar-1.6.0-show-nodisplay-true-applications.patch)
sha256sums=('354897fbde4d3f089c06c38b57816f455c2907806725906426440e1084c1d63a'
            'f7377aad1eb60420d0c1c878c3916913934f994df810f3a60d580fc2be3b80c0')

groups=('xfce4-devel')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname" "$_pkgname-git")

build() {
  cd "$srcdir/Thunar-$pkgver"

  # https://bugzilla.xfce.org/show_bug.cgi?id=9595
  patch -Np1 -i "$srcdir/thunar-1.6.0-show-nodisplay-true-applications.patch"

  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib \
    --localstatedir=/var \
    --disable-static \
    --enable-gio-unix \
    --enable-dbus \
    --enable-startup-notification \
    --enable-gudev \
    --enable-notifications \
    --enable-exif \
    --enable-pcre \
    --enable-gtk-doc \
    --disable-debug
  make
}

package() {
  cd "$srcdir/Thunar-$pkgver"

  make DESTDIR=${pkgdir} install
  sed -i 's:x-directory/gnome-default-handler;::' \
    "$pkgdir/usr/share/applications/Thunar-folder-handler.desktop"
}

# vim:set ts=2 sw=2 et:
