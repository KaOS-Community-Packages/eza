pkgname=eza
pkgver=0.18.14
pkgrel=1
pkgdesc="A modern replacement for ls"
url="https://github.com/eza-community/eza"
arch=(x86_64)
license=(MIT)
depends=(gcc-libs glibc libgit2)
makedepends=(rust)
source=("$url/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha256sums=('f8f42ed466c02eaaa2b157ef976d29f1c38a6ff13064be52baed70e4943f2481')
b2sums=('c27852afc92454d684390f737f1b70c7bb4b2a6c50ae68fd61ae99d7a1af2b8c14ea9ebfec129f3861a1a8bd5d569467b72416a4d4dc6ceabbc8353396523d62')

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

