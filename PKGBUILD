# Maintainer: Přemysl Janouch <p.janouch@gmail.com>

pkgname=logdiag-git
_pkgname=logdiag
pkgver=v0.1.2.r99.ge74d582
pkgrel=1
pkgdesc="Schematic editor"
url="https://github.com/pjanouch/logdiag"
arch=('i686' 'x86_64')
license=('BSD')
options=(zipman)
conflicts=('logdiag')
provides=('logdiag')
makedepends=('cmake' 'pkg-config' 'git')
depends=('gtk3' 'lua' 'json-glib')
install=logdiag.install
source=('git+https://github.com/pjanouch/logdiag.git')
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd $srcdir/$_pkgname
  mkdir build
  cd build
  cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
  make
}

package() {
  cd $srcdir/$_pkgname/build
  make install DESTDIR=$pkgdir
}
