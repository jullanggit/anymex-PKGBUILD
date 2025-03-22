# Based off of: https://daveparrish.net/posts/2019-11-16-Better-AppImage-PKGBUILD-template.html
# Maintainer: jullanggit <jullanggit@proton.me>

pkgname=anymex
_PkgName=AnymeX # capitalised name
pkgver=2.9.3_hotfix
pkgrel=3
arch=(x86_64) # not sure if arm is also supported on linux
pkgdesc='An Open Source app for Tracking Multi Service (AL, MAL, SIMKL)'
url="https://github.com/RyanYuuki/$_PkgName"
license=(MIT)
depends=(mpv) # not sure if that's all
provides=("$pkgname=$pkgver")
conflicts=(anymex)
_appimage=$_PkgName.AppImage
source=($_appimage::$url/releases/download/v${pkgver//_/-}/$_PkgName-Linux.AppImage)
noextract=($_appimage)
b2sums=('SKIP')

prepare() {
  chmod +x $_appimage
  ./$_appimage --appimage-extract >/dev/null
}

build() {
  # Fix permissions; .AppImage permissions are 700 for all directories
  chmod -R a-x+rX squashfs-root/usr
}

package() {
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

  # Icon images
  install -dm755 "$pkgdir/usr/share/"
  cp -a "$srcdir/squashfs-root/usr/share/icons" "$pkgdir/usr/share/"

  # wrapper script
  install -Dm755 /dev/stdin "$pkgdir/usr/bin/$pkgname" <<'EOF'
#!/bin/sh
export LD_LIBRARY_PATH="/usr/lib/anymex:${LD_LIBRARY_PATH}"
exec /usr/bin/anymex.bin "$@"
EOF

  # actual binary
  install -Dm755 "$srcdir/squashfs-root/usr/bin/anymex" "$pkgdir/usr/bin/$pkgname.bin"

  # data
  install -dm755 "$pkgdir/usr/bin/data/"
  mv $srcdir/squashfs-root/usr/bin/data/* "$pkgdir/usr/bin/data/" # using /usr/share/anymex doesnt work

  # lib
  install -dm755 "$pkgdir/usr/bin/lib/"
  mv $srcdir/squashfs-root/usr/bin/lib/* "$pkgdir/usr/bin/lib/" # using /usr/lib/anymex doesnt work
}
