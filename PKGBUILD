pkgname=eza
pkgver=0.20.11
pkgrel=1
pkgdesc='A modern replacement for ls'
arch=('x86_64')
url='https://github.com/eza-community/eza'
license=('EUPL-1.2')
depends=('gcc-libs' 'glibc' 'libgit2')
makedepends=('rust')
source=("${url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha256sums=('1a3ec9fb87c61e2369b46945ff1fafb7cbb5e6cb4693bb59003f4b628a93a04c')

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
  install -Dm644 LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
