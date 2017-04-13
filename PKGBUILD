# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=5.33.0
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=('any')
url='https://community.kde.org/Frameworks'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx' 'python-requests') # qt5-tools for QtHelp pages
source=("https://download.kde.org/stable/frameworks/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz"{,.sig}
        fix-python-bindings-generation.patch ECM-no-init.py.patch)
sha256sums=('f3ff5e36c45ff579a742de700680678211cc90d8132af18f3a1c68f4f36b6a04'
            'SKIP'
            '51cc99dad7c60c8f3f4ffddfd75d781d00e4ac83638a6daf914bc9a3fd8a1502'
            '5695e45c7621a00c0bca28f058c13b5d524f963a00b53337c8cefcdaf22c4b52')
validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>

prepare() {
  mkdir -p build

  cd $pkgname-$pkgver
  sed -e 's|/usr/bin/env python|/usr/bin/env python2|' -i find-modules/*.py
# Fix Ubuntu-specific code https://bugs.kde.org/show_bug.cgi?id=372311
  patch -p1 -i ../fix-python-bindings-generation.patch
# Don't create __init__.py, depend on python-pykf5 instead
  patch -p1 -i ../ECM-no-init.py.patch
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
