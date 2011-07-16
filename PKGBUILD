# Maintainer: Tobias Powalowski <tpowa@archlinux.org>

pkgname=ocaml	
pkgver=3.12.1
pkgrel=1
pkgdesc="A functional language with OO extensions"
arch=('i686' 'x86_64')
license=('LGPL2' 'custom: QPL-1.0')
url="http://caml.inria.fr/"
depends=('gdbm')
makedepends=('tk' 'ncurses>=5.6-7' 'libx11')
optdepends=('ncurses: advanced ncurses features' 'tk: advanced tk features')
source=(http://caml.inria.fr/distrib/ocaml-3.12/${pkgname}-${pkgver}.tar.gz)
options=('!makeflags' '!emptydirs')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure -prefix /usr 
  make world.opt
  make PREFIX="${pkgdir}/usr" MANDIR="${pkgdir}/usr/share/man" install
   
  # Save >10MB with this one, makepkg only strips debug symbols.
  #find ${startdir}/pkg/usr/lib -type f -name '*.so.*' -exec strip --strip-unneeded {} \;

  # install license
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/"
}
md5sums=('814a047085f0f901ab7d8e3a4b7a9e65')
