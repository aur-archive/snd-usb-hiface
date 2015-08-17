# $Id$
# Maintainer: Quan Guo <guotsuan@gmail.com>

pkgname=snd-usb-hiface
pkgver=2013.12.27.g3b80b85
pkgrel=1
pkgdesc="A kernel module for Hiface USB interface, Hi-End S/PDIF Output Interface"
url="http://www.m2tech.biz/hiface.html"
license=("GPL")
arch=('i686' 'x86_64')
depends=('glibc' 'linux')
makedepends=('linux-headers')
source=('git://github.com/panicking/snd-usb-asyncaudio.git')
md5sums=("SKIP")

_major=$(uname -r | cut -d '.' -f-2)
_extramodules=extramodules-${_major}-ARCH

_gitname="snd-usb-asyncaudio"

install=${pkgname}.install



pkgver() {
  cd "${srcdir}/${_gitname}"
      git log -1 --format="%cd.g%h" --date=short | sed 's/-/./g'
}

build() {
  cd $srcdir/$_gitname

  local _kernver="$(cat /usr/lib/modules/$_extramodules/version || true)"
  make
}

package() {
  cd ${srcdir}/${_gitname}
  install -Dm644 $pkgname.ko "$pkgdir/usr/lib/modules/$_extramodules/$pkgname.ko"
  find "$pkgdir" -name '*.ko' -exec gzip -9 {} +

 # Write $_extramodules to .install
  sed -i "s/_extramodules='.*'/_extramodules='${_extramodules}'/" "${startdir}/${install}"
}


