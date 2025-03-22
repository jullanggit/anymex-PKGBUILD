# Based off of: https://daveparrish.net/posts/2019-11-16-Better-AppImage-PKGBUILD-template.html
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
_appimage=$_PkgName.AppImage
source=($_appimage::$url/releases/download/v${pkgver//_/-}/$_PkgName-Linux.AppImage)
noextract=($_appimage)
b2sums=('SKIP')

prepare() {
  chmod +x "${_appimage}"
  ./"${_appimage}" --appimage-extract
}

build() {
  # Fix permissions; .AppImage permissions are 700 for all directories
  chmod -R a-x+rX squashfs-root/usr
}

package() {
  # Desktop file
  install -Dm644 "${srcdir}/squashfs-root/${pkgname}.desktop" \
    "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  # Icon images
  mkdir -p "${pkgdir}/usr/share/"
  cp -a "${srcdir}/squashfs-root/usr/share/icons" "${pkgdir}/usr/share/"

  # binary
  install -Dm755 "$srcdir/squashfs-root/usr/bin/anymex" "$pkgdir/usr/bin/$pkgname"

  # data
  mkdir -p "$pkgdir/usr/share/$pkgname/"
  cp -a $srcdir/squashfs-root/usr/bin/data/* "${pkgdir}/usr/share/$pkgname/"

  # lib
  mkdir -p "$pkgdir/usr/lib/$pkgname/"
  cp -a $srcdir/squashfs-root/usr/bin/lib/* "${pkgdir}/usr/lib/$pkgname/"
}
