# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025
#                Tomislav Ivek
#                Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer:
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer:
#   Tomislav Ivek
#     <tomislav.ivek@gmail.com>

_evmfs_available="$( \
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg="node-semver"
pkgname=(
  "${_py}-${_pkg}"
)
pkgver=0.8.1
pkgrel=2
_pkgdesc=(
  "python version of node-semver"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
_ns="podhmo"
url="${_http}/${_ns}/${pkgname}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
conflicts=(
  "${_py}-semver"
)
makedepends=(
  "${_py}-setuptools"
)
_tarname="${pkgname}-${pkgver}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_archive_sum="1ff28cdf1f7e10d853e0d147b0cb170e42f842cc8bcc481b5e6b166f34aa8fee"
_evmfs_archive_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sum}"
_evmfs_archive_src="${_tarname}.zip::${_evmfs_archive_uri}"
_archive_sig_sum="e301bdd15c2ae191773c7b7435d08c84d085cce5a907e0c0cab0ece92aff958b"
_archive_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sig_sum}"
_archive_sig_src="${_tarname}.zip.sig::${_archive_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
  _src="${_evmfs_archive_src}"
  source+=(
    "${_archive_sig_src}"
  )
  sha256sums+=(
    "${_archive_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  _uri="${url}/archive/${pkgver}.tar.gz"
  _src="${_tarname}.tar.gz::${_uri}"
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_archive_sum}"
)
sha512sums=(
  '5a988755ed97aa1ba9b97595738200821787c2cc71f40198cffdc22c4b823fe132668946ecc3f0fb66d6c33fe0ec7bdcfa9c9794e3d382b38f8551d15d4af5e6'
)

build() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    "setup.py" \
      build
}

package() {
  cd \
    "$srcdir/${_tarname}"
  "${_py}" \
    "setup.py" \
      install \
        --optimize=1 \
        --root="${pkgdir}"
  install \
    -vDm644 \
      "${srcdir}/${_tarname}/LICENSE" \
      "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
