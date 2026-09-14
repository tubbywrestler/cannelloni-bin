# Maintainer: pineappletoad

pkgname=cannelloni-bin
pkgver=2.1.2
_pkgrel_src=2
pkgrel=1
pkgdesc="cannelloni is written in C++11 and uses UDP, TCP or SCTP to transfer CAN frames between two machines. (precompiled)"
arch=('x86_64' 'armv7h')
url="https://github.com/mguentner/cannelloni"
license=('GPL-2.0-only')
options=('!debug')
provides=('cannelloni')
conflicts=('cannelloni')
# armv7h is cross-compiled with -DSCTP_SUPPORT=OFF (no ARM-cross build of
# lksctp-tools available), so it doesn't need or link against it - UDP/TCP
# transport, cannelloni's primary use case, is unaffected.
depends_x86_64=('libgcc_s.so' 'libstdc++.so' 'lksctp-tools')
depends_armv7h=('libgcc_s.so' 'libstdc++.so')

# x86_64: a full pacman package built natively (via aur-bin-chicken), re-extracted.
# armv7h: a plain tarball of a cross-compiled install tree (arm-linux-gnueabihf-*-bin
# toolchain, built in CI on an x86_64 runner) - no native build happens on armv7h
# at all, this is purely a repackaging step there too.
source_x86_64=("https://github.com/tubbywrestler/cannelloni-bin/releases/download/${pkgver}-${_pkgrel_src}/cannelloni-${pkgver}-${_pkgrel_src}-x86_64.pkg.tar.zst")
sha256sums_x86_64=('0f05364ca1848b4a28bb86ddeabd1995f72f39447998e264eda60b2f8de313cf')
source_armv7h=("https://github.com/tubbywrestler/cannelloni-bin/releases/download/${pkgver}-${_pkgrel_src}/cannelloni-${pkgver}-${_pkgrel_src}-armv7h.tar.zst")
sha256sums_armv7h=('0f05364ca1848b4a28bb86ddeabd1995f72f39447998e264eda60b2f8de313cf')

package() {
    if [ "${CARCH}" = "armv7h" ]; then
        cp -a "${srcdir}/usr" "${pkgdir}/"
    else
        bsdtar -xf "${srcdir}/cannelloni-${pkgver}-${_pkgrel_src}-x86_64.pkg.tar.zst" -C "${pkgdir}" --exclude .PKGINFO --exclude .BUILDINFO --exclude .MTREE
    fi
}
