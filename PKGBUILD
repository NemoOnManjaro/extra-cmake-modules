# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=5.30.0
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=('any')
url='https://community.kde.org/Frameworks'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx' 'python-requests') # qt5-tools for QtHelp pages
source=("http://download.kde.org/stable/frameworks/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz"{,.sig}
        fix-python-bindings-generation.patch ECM-no-init.py.patch
        python-bindings-c++14.patch::"https://cgit.kde.org/extra-cmake-modules.git/patch/?id=8aa68434")
md5sums=('3678f6f17ff10ba5022fc1800028538f'
         'SKIP'
         '5a704fb81d356a678d2affd403d8f468'
         '63582bd0c967a2315736da7c2cb48d81'
         'a898dc73e16a0f60bdf339a2a9aaf0cf')
validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>

prepare() {
  mkdir -p build

  cd $pkgname-$pkgver
  sed -e 's|/usr/bin/env python|/usr/bin/env python2|' -i find-modules/*.py
# Fix Ubuntu-specific code https://bugs.kde.org/show_bug.cgi?id=372333 https://bugs.kde.org/show_bug.cgi?id=372311
  patch -p1 -i ../fix-python-bindings-generation.patch
# Don't create __init__.py, depend on python-pykf5 instead
  patch -p1 -i ../ECM-no-init.py.patch
# Pass -std=gnu++14 flags to clang for Python bindings generation https://bugs.kde.org/show_bug.cgi?id=374801
  patch -p1 -i ../python-bindings-c++14.patch
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
