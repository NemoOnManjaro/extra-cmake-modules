# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=5.29.0
pkgrel=2
pkgdesc='Extra modules and scripts for CMake'
arch=('any')
url='https://community.kde.org/Frameworks'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx' 'python-requests') # qt5-tools for QtHelp pages
source=("http://download.kde.org/stable/frameworks/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz"{,.sig}
        fix-python-bindings-generation.patch)
md5sums=('dd3e13ee27fb421a9d215fc708ae02b3'
         'SKIP'
         '5a704fb81d356a678d2affd403d8f468')
validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>

prepare() {
  mkdir -p build

  cd $pkgname-$pkgver
  sed -e 's|/usr/bin/env python|/usr/bin/env python2|' -i find-modules/*.py
# Fix Ubuntu-specific code https://bugs.kde.org/show_bug.cgi?id=372333 https://bugs.kde.org/show_bug.cgi?id=372311
  patch -p1 -i ../fix-python-bindings-generation.patch
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
