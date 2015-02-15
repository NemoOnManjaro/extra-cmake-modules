# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=1.7.0
_pkgver=5.7.0
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=('i686' 'x86_64') # 'any' is broken, see https://git.reviewboard.kde.org/r/118498/
url='https://projects.kde.org/projects/kdesupport/extra-cmake-modules'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx') # qt5-tools for QtHelp pages
source=("http://download.kde.org/stable/frameworks/${_pkgver%.*}/${pkgname}-${pkgver}.tar.xz")
md5sums=('45fd1e6f38b23b00983e5eab9ba61d15')

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
