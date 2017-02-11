# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=5.31.0
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=('any')
url='https://community.kde.org/Frameworks'
license=('LGPL')
depends=('cmake')
makedepends=('python-sphinx' 'python-requests') # qt5-tools for QtHelp pages
source=("http://download.kde.org/stable/frameworks/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz"{,.sig}
        fix-python-bindings-generation.patch ECM-no-init.py.patch
        2e20aeab.patch::"https://cgit.kde.org/extra-cmake-modules.git/patch/?id=2e20aeab")
md5sums=('74d7c29138168f9a62fe475705c0b351'
         'SKIP'
         '4e53103b3e132613dd2e2ae9cf4c7c8b'
         'fe4ad511edb544434e7afaeba12dd460'
         'e5b690bd3530d310a91ae7c7f19dc61a')
validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>

prepare() {
  mkdir -p build

  cd $pkgname-$pkgver
  sed -e 's|/usr/bin/env python|/usr/bin/env python2|' -i find-modules/*.py
# Fix Ubuntu-specific code https://bugs.kde.org/show_bug.cgi?id=372311
  patch -p1 -i ../fix-python-bindings-generation.patch
# Don't create __init__.py, depend on python-pykf5 instead
  patch -p1 -i ../ECM-no-init.py.patch
# Revert commit that breaks kcoreaddons python bindings build
  patch -Rp1 -i ../2e20aeab.patch
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
