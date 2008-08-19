#Maintainer: Tobias Powalowski <tpowa@archlinux.org>

pkgname=ocaml	
pkgver=3.10.2
pkgrel=2
pkgdesc="Ocaml compiler - Ocaml is a functional language with OO extensions"
arch=(i686 x86_64)
license=('LGPL2' 'custom: QPL-1.0')
url="http://caml.inria.fr/"
depends=('gdbm')
makedepends=('tk' 'ncurses=5.6-7' 'libx11')
optdepends=('ncurses=5.6-7: advanced ncurses features' 'tk: advanced tk features')
source=(http://caml.inria.fr/distrib/ocaml-3.10/$pkgname-$pkgver.tar.gz)
options=('!makeflags' '!emptydirs')
md5sums=('52c795592c90ecb15c2c4754f04eeff4')

build() {
  cd $srcdir/$pkgname-$pkgver
  ./configure -prefix /usr
  make world.opt || return 1
  make PREFIX=$pkgdir/usr install || return 1
   
# Save >10MB with this one, makepkg only strips debug symbols.
 find ${startdir}/pkg/usr/lib -type f -name '*.so.*' -exec strip --strip-unneeded {} \;

# install license
install -D -m 644 $startdir/src/$pkgname-$pkgver/LICENSE $startdir/pkg/usr/share/licenses/ocaml/LICENSE
}
