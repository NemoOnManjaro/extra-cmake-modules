# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=plasma2tp.r0.g83f4d25
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=('any')
url='https://projects.kde.org/projects/kdesupport/extra-cmake-modules'
license=('LGPL')
depends=('cmake')
makedepends=('git')
source=('git://anongit.kde.org/extra-cmake-modules.git#tag=plasma2tp')
md5sums=('SKIP')

pkgver() {
  cd extra-cmake-modules
  git describe --long | sed -E 's/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../extra-cmake-modules \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
}
