# Maintainer: jullanggit <jullanggit@proton.me>

pkgname=anymex
_PkgName=AnymeX # capitalised name
pkgver=2.9.3_hotfix
pkgrel=1
arch=(x86_64) # not sure if arm is also supported on linux
pkgdesc='An Open Source app for Tracking Multi Service (AL, MAL, SIMKL)'
url="https://github.com/RyanYuuki/${_PkgName}"
license=(MIT)
provides=("${pkgname}=${pkgver}")
conflicts=(anymex)
source=($_PkgName.AppImage::$url/releases/download/v${pkgver//_/-}/$_PkgName-Linux.AppImage)
b2sums=('SKIP')

package() {
  # binary
  install -Dm755 "$srcdir/anymex" "$pkgdir/usr/bin/$pkgname"

  # lib
  install -Dm755 "$pkgdir/usr/lib/$pkgname/"
  cp

  # data
  install -Dm755 "$pkgdir/usr/share/$pkgname/"
}
