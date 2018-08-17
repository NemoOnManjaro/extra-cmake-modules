# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=extra-cmake-modules
pkgver=5.49.0
pkgrel=1
pkgdesc='Extra modules and scripts for CMake'
arch=(any)
url='https://community.kde.org/Frameworks'
license=(LGPL)
depends=(cmake)
makedepends=(python-sphinx python-requests qt5-tools)
groups=(kf5)
source=("https://download.kde.org/stable/frameworks/${pkgver%.*}/$pkgname-$pkgver.tar.xz"{,.sig}
        fix-python-bindings-generation.patch ECM-no-init.py.patch ecm-python3.patch ecm-scoped-enums.patch)
sha256sums=('c09fb851751f2e1c1231130dbce62d5dab396444fce7ed18662ada9ebd7ced1e'
            'SKIP'
            '5ff36668bd66a9adc35cf72c8161671977418f1fe98f1512d4427b0dd21a0e1e'
            '5695e45c7621a00c0bca28f058c13b5d524f963a00b53337c8cefcdaf22c4b52'
            'eae8d9f49209ee333c891b319a990670c16e151e049ded1741be32a7ca0e32ed'
            '755273ea983edbcc378e50bdecbfd77be181728445d36a173fcae13179c76f65')
validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>

prepare() {
  mkdir -p build

  cd $pkgname-$pkgver
  sed -e 's|/usr/bin/env python|/usr/bin/env python2|' -i find-modules/*.py
# Fix Ubuntu-specific code https://bugs.kde.org/show_bug.cgi?id=372311
  patch -p1 -i ../fix-python-bindings-generation.patch
# Don't create __init__.py
  patch -p1 -i ../ECM-no-init.py.patch
# Port python binding generation scripts to python3
  patch -p1 -i ../ecm-python3.patch
# Support scoped enums https://phabricator.kde.org/D14908
  patch -p1 -i ../ecm-scoped-enums.patch
}

build() {
  cd build
  cmake ../$pkgname-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DBUILD_HTML_DOCS=OFF \
    -DBUILD_QTHELP_DOCS=ON \
    -DBUILD_TESTING=OFF
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
