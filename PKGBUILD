# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Marenz <aur@supradigital.org>
# Maintainer: Kamil Śliwak <cameel2+aur/at/gmail/com>

_git="true"
_offline="false"
_pkg=evmone
pkgname="${_pkg}"
pkgver=0.13.0
_commit="7961b60012220bf25d15569acd18c68ced96473b"
pkgrel=1
_pkgdesc=(
  "Fast Ethereum Virtual"
  "Machine implementation"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'i686'
  'arm'
  'armv7l'
  'armv6l'
  'aarch64'
  'mips'
  'powerpc'
  'pentium4'
)
_http="https://github.com"
_ns="ethereum"
url="${_http}/${_ns}/${_pkg}"
license=(
  'Apache'
)
depends=()
makedepends=(
  'cmake'
  'gcc'
)
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  _sum="SKIP"
elif [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _src="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum='955be86b162169b67c4497bfc3db2d03263f2e47a48a3bb6586d59b014595c31'
  fi
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)

build ()
{
  echo \
    "${PWD}"
  cd \
    "${_tarname}"
  git \
    submodule \
      update \
      --init
  mkdir \
    build -p
  cd \
    build
  cmake \
    .. \
    -DEVMONE_TESTING=OFF \
    -DCMAKE_INSTALL_PREFIX=/usr
  make
}

package ()
{
  cd \
    "${_tarname}/build"
  make \
    DESTDIR="${pkgdir}" \
    prefix=/usr \
    install
}
