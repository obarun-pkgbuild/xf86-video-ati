# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/xf86-video-ati
# 						Maintainer: Jan de Groot <jgc@archlinux.org>
# 						Contributor: Alexander Baldeck <alexander@archlinux.org>

pkgname=xf86-video-ati
pkgver=18.0.0
pkgrel=2
epoch=1
pkgdesc="X.org ati video driver"
arch=('x86_64')
url="https://xorg.freedesktop.org/"
license=('custom')
depends=('mesa')
makedepends=('xorg-server-devel' 'X-ABI-VIDEODRV_VERSION=23')
conflicts=('xorg-server<1.19.0' 'X-ABI-VIDEODRV_VERSION<23' 'X-ABI-VIDEODRV_VERSION>=24')
groups=('xorg-drivers')
source=(${url}/releases/individual/driver/${pkgname}-${pkgver}.tar.bz2)
sha512sums=('a9a634091f208099885039d42433cee061e03968417c0d535691833abcc9162d8d0a46f99bac902f0885beb14dcc9a011d104b535ffe492562fd5bb740ad4721')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

build() {
  cd ${pkgname}-${pkgver}
  
  # Since pacman 5.0.2-2, hardened flags are now enabled in makepkg.conf
  # With them, module fail to load with undefined symbol.
  # See https://bugs.archlinux.org/task/55102 / https://bugs.archlinux.org/task/54845
  export CFLAGS=${CFLAGS/-fno-plt}
  export CXXFLAGS=${CXXFLAGS/-fno-plt}
  export LDFLAGS=${LDFLAGS/,-z,now}

  ./configure --prefix=/usr 
  make
}

check() {
  cd ${pkgname}-${pkgver}
  make check
}

package() {
  cd ${pkgname}-${pkgver}

  make "DESTDIR=${pkgdir}" install
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"
}
