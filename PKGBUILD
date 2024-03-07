# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  Pellegrino Prevete (dvorak) <cGVsbGVncmlub3ByZXZldGVAZ21haWwuY29tCg== | base -d>
# Maintainer:  Truocolo <truocolo@aol.com>
# Maintainer: Jürgen Hötzel <juergen@archlinux.org>

pkgbase='ocaml'
pkgname=(
  'ocaml'
  'ocaml-compiler-libs'
)
pkgver=5.1.0
pkgrel=1
pkgdesc="A functional language with OO extensions"
arch=(
  'x86_64'
  'arm'
)
license=(
  'LGPL2.1'
  'custom: QPL-1.0'
)
url="https://caml.inria.fr/"
makedepends=(
  'ncurses>=5.6-7'
)
optdepends=(
  'ncurses: advanced ncurses features' 'tk: advanced tk features'
)
source=(
  https://caml.inria.fr/distrib/ocaml-${pkgver%.*}/${pkgname}-${pkgver}.tar.xz)
sha512sums=(
  '23579b76592e225f2ddec58d78084dfd11befede18b61be71d3896fd72a90cc0fe4fb1f64a7dcbc83239ed69ec4254e13ab86fd810671851044c2a353da3adc5')
options=(
  '!makeflags'
  '!emptydirs'
  'staticlibs'
)

_bin="$( \
  dirname \
    "$( \
      command \
        -v \
          cc \
          gcc)")"
_usr="$( \
  dirname \
    "${_bin}")"

build() {
  local \
    _configure_opts=()
    _cppflafs=() \
    _cflags=() \
    _cxxflags=() \
    _ldflags=()
  cd \
    "${srcdir}/${pkgname}-${pkgver}"
  _configure_opts=(
    --prefix="/usr"
    --mandir="/usr/share/man"
  )
  [[ "${CARCH}" == 'x86_64' ]] && \
    _configure_opts+=(
      -enable-frame-pointers
    )
  _cflags=(
    "${CFLAGS}"
    '-ffat-lto-objects'
    "-I${_usr}/include/pthread.h"
  )
  _cxxflags=(
    "${CXXFLAGS}"
    '-ffat-lto-objects'
  )
  _ldflags=(
    "${LDFLAGS}"
    '-lpthread'
  )
  CFLAGS="${_cflags[*]}" \
  CXXFLAGS="${_cxxflags[*]}" \
  LDFLAGS="${_ldflags[*]}" \
  ./configure \
    "${_configure_opts[@]}"
  CFLAGS="${_cflags[*]}" \
  CXXFLAGS="${_cxxflags[*]}" \
  LDFLAGS="${_ldflags[*]}" \
  make \
    --debug=v \
    world.opt
}

package_ocaml() {
  cd \
    "${srcdir}/${pkgbase}-${pkgver}"
  make \
    DESTDIR="${pkgdir}" \
    install
  # Save >10MB with this one,
  # makepkg only strips debug symbols.
  # find \
  #   "${pkgdir}/usr/lib" \
  #   -type f \
  #   -name '*.so.*' \
  #   -exec strip \
  #   --strip-unneeded {} \;
  # install license
  install \
    -m755 \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -m644 \
    LICENSE \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
  # remove compiler libs
  rm \
    -rf \
    "${pkgdir}/usr/lib/ocaml/compiler-libs"
}

package_ocaml-compiler-libs() {
  pkgdesc="Several modules used internally by the OCaml compiler"
  license=(
    'custom: QPL-1.0'
  )
  depends=(
    'ocaml'
  )
  optdepends=()
  cd \
    "${srcdir}/${pkgbase}-${pkgver}"
  make \
    DESTDIR="${pkgdir}" \
    install
  # Remove non-compiler-libs
  find \
    "${pkgdir}/usr/lib/ocaml/" \
    -mindepth 1 \
    -maxdepth 1 \
    -not -name "compiler-libs" \
    -execdir \
      rm \
        -rf \
	"{}" \
	"+"
  rm \
    -rf \
    "${pkgdir}/usr/bin" \
    "${pkgdir}/usr/share"
  install \
    -dm755 \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -m644 \
    LICENSE \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim:set sw=2 sts=-1 et:
