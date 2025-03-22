# Based off of: https://daveparrish.net/posts/2019-11-16-Better-AppImage-PKGBUILD-template.html
# Maintainer: jullanggit <jullanggit@proton.me>

pkgname=anymex-bin
_PkgName=AnymeX # capitalised name
pkgver=2.9.3_hotfix
pkgrel=4
arch=(x86_64) # not sure if arm is also supported on linux
pkgdesc='An Open Source app for Tracking Multi Service (AL, MAL, SIMKL)'
url="https://github.com/RyanYuuki/$_PkgName"
license=(MIT)
depends=(
  'libepoxy'
  'gdk-pixbuf2'
  'pango'
  'webkit2gtk-4.1'
  'harfbuzz'
  'libsoup3'
  'glibc'
  'fontconfig'
  'cairo'
  'hicolor-icon-theme'
  'glib2'
  'gcc-libs'
  'mpv'
  'zlib-ng-compat'
  'gtk3'
  'at-spi2-core'
)
conflicts=(anymex)
_appimage="$_PkgName-$pkgver.AppImage"
source=($_appimage::$url/releases/download/v${pkgver//_/-}/$_PkgName-Linux.AppImage)
noextract=($_appimage)
sha256sums=('a177b936d7a061c2acf64caff40402b258ee4af277ab3b1e3f34bc2eac6f1f88')

prepare() {
  chmod +x $_appimage
  ./$_appimage --appimage-extract >/dev/null
}

build() {
  # Fix permissions; .AppImage permissions are 700 for all directories
  chmod -R a-x+rX squashfs-root/usr

  chmod +x squashfs-root/usr/bin/anymex
}

package() {
  install -dm755 "$pkgdir/usr/"
  mv "$srcdir"/squashfs-root/usr/* "$pkgdir/usr/"

  # Desktop file
  install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/$pkgname.desktop" <<EOF
[Desktop Entry]
Version=$pkgver
Type=Application
Name=$_PkgName
GenericName=$_PkgName
Comment=$pkgdesc
Exec=$pkgname
Icon=$pkgname
Terminal=false
Categories=Utility;Application;
Keywords=$pkgname;anime
StartupNotify=true
EOF

}
