# Maintainer: Tobias Powalowski <tpowa@archlinux.org>

pkgname=ocaml	
pkgver=3.12.0
pkgrel=1
pkgdesc="A functional language with OO extensions"
arch=('i686' 'x86_64')
license=('LGPL2' 'custom: QPL-1.0')
url="http://caml.inria.fr/"
depends=('gdbm')
makedepends=('tk' 'ncurses>=5.6-7' 'libx11')
optdepends=('ncurses: advanced ncurses features' 'tk: advanced tk features')
source=(http://caml.inria.fr/distrib/ocaml-3.12/$pkgname-$pkgver.tar.gz)
options=('!makeflags' '!emptydirs')

build() {
  cd $srcdir/$pkgname-$pkgver
  ./configure -prefix /usr 
  make world.opt || return 1
  make PREFIX=$pkgdir/usr MANDIR=$pkgdir/usr/share/man install || return 1
   
# Save >10MB with this one, makepkg only strips debug symbols.
 find ${startdir}/pkg/usr/lib -type f -name '*.so.*' -exec strip --strip-unneeded {} \;

# install license
install -D -m 644 $startdir/src/$pkgname-$pkgver/LICENSE $startdir/pkg/usr/share/licenses/ocaml/LICENSE
}
md5sums=('3ba7cc65123c3579f14e7c726d3ee782')
