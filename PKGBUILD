pkgname=eza
pkgver=0.19.4
pkgrel=1
pkgdesc='A modern replacement for ls'
arch=('x86_64')
url='https://github.com/eza-community/eza'
license=('MIT')
depends=('gcc-libs' 'glibc' 'libgit2')
makedepends=('rust')
source=("${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha256sums=('c0094b3ee230702d4dd983045e38ea2bd96375c16381c0206c88fae82fb551a4')

prepare() {
  cd "${pkgname}-${pkgver}"
  cargo fetch --locked --target "$(rustc -vV | sed -n 's/host: //p')"
}

build() {
  cd "${pkgname}-${pkgver}"
  CFLAGS+=' -ffat-lto-objects'
  cargo build --frozen --release
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 "target/release/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  ln -s eza "${pkgdir}/usr/bin/exa"
  install -Dm644 "completions/bash/${pkgname}" -t "${pkgdir}/usr/share/bash-completion/completions"
  install -Dm644 "completions/zsh/_${pkgname}" -t "${pkgdir}/usr/share/zsh/site-functions/"
  install -Dm644 "completions/fish/${pkgname}.fish" -t "${pkgdir}/usr/share/fish/vendor_completions.d"
  install -Dm644 LICENCE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
