# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=1.0.0
_pkgver=5.0.0
pkgrel=1
pkgdesc='Extra CMake modules'
arch=('i686' 'x86_64') # 'any' is broken, see https://git.reviewboard.kde.org/r/118498/
url='https://projects.kde.org/projects/kdesupport/extra-cmake-modules'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx') # qt5-tools for QtHelp pages
source=("http://download.kde.org/stable/frameworks/${_pkgver}/${pkgname}-${pkgver}.tar.xz")
md5sums=('a7b9e8756fdc2b3a8518ad9f9d21dfd5')

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
