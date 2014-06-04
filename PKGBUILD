# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=0.0.14
_pkgver=4.100.0
pkgrel=1
pkgdesc='Extra CMake modules'
arch=('any')
url='https://projects.kde.org/projects/kdesupport/extra-cmake-modules'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx') # qt5-tools for QtHelp pages
source=("http://download.kde.org/unstable/frameworks/${_pkgver}/${pkgname}-${pkgver}.tar.xz")
md5sums=('14a6f6c411af4797af6c56099fea4ed0')

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../${pkgname}-${pkgver} \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_HTML_DOCS=OFF
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
}
