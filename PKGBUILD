# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=5.24.0
pkgrel=2
pkgdesc='Extra modules and scripts for CMake'
arch=('any')
url='https://community.kde.org/Frameworks'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx') # qt5-tools for QtHelp pages
source=("http://download.kde.org/stable/frameworks/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz"
        pri-install-dir.patch::"https://quickgit.kde.org/?p=extra-cmake-modules.git&a=commitdiff&h=5bb92992&o=plain")
md5sums=('cd3b0c844234ad29cfdba89d63ccb2ae'
         '2357eb8f8ecff829e29b2d3e5777c8c8')

prepare() {
  mkdir -p build

# Workaround wrong .pri install dir https://bugs.kde.org/show_bug.cgi?id=363348
  cd $pkgname-$pkgver
  patch -p1 -i ../pri-install-dir.patch
}

build() {
  cd build
  cmake ../${pkgname}-${pkgver} \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_HTML_DOCS=OFF \
    -DBUILD_TESTING=OFF
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
}
