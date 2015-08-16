# Maintainer: SpepS <dreamspepser at yahoo dot it>

pkgname=neil
pkgver=0.13_hg
pkgrel=4
pkgdesc="A modular Buzz-like tracker, fork of aldrin."
arch=(i686 x86_64)
url="http://sites.google.com/site/neilsequencer/"
license=('GPL')
depends=('pygtk' 'python2-numpy' 'python-opengl' 'wxpython' 'liblo'
         'libmad' 'gtkglarea' 'gtkglext' 'fftw' 'mpg123' 'jack'
         'hicolor-icon-theme' 'desktop-file-utils')
makedepends=('scons' 'ladspa' 'dssi' 'boost' 'xmlto' 'docbook-xsl')
provides=('libneil' 'libneil-hg')
conflicts=('neil-hg' 'libneil' 'libneil-hg')
install="$pkgname.install"
source=("https://bitbucket.org/bucket_brigade/$pkgname/get/tip.tar.bz2")
md5sums=(`wget -qO- $source | md5sum | cut -c -32`)

build() {
  cd "$srcdir/bucket"*

  # python2 build fix
  sed -i "s|'python |'python2 |g" libneil/SConscript

  scons configure PREFIX=/usr
  scons
}

package() {
  cd "$srcdir/bucket"*

  scons install DESTDIR="$pkgdir/"
  
  # python2 fix
  sed -i "s|env python|&2|" `grep -rl "env python" "$pkgdir"`

  # config file path fix
  sed -i "s|$pkgdir||" "$pkgdir/etc/neil/path.cfg"
}

# vim:set ts=2 sw=2 et:
