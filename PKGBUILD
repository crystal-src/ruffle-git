pkgname=ruffle-git
pkgver=0.1.0.r7489.286755962
pkgrel=1
arch=('x86_64')
url="https://github.com/ruffle-rs/ruffle"
pkgdesc="A Flash Player emulator written in Rust"
license=('Apache' 'MIT')
depends=('openssl' 'libxcb' 'zlib' 'alsa-lib')
makedepends=('rust' 'cargo' 'git' 'libx11' 'python')
provides=('ruffle')
conflicts=('ruffle')
source=("${pkgname%-git}::git+$url")
sha256sums=('SKIP')

pkgver() {
    cd "${pkgname%-git}"/desktop
    printf "%s.r%s.%s" $(awk '/^version/ {gsub(/"/, ""); print $3}' Cargo.toml) "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build(){
    cd "${pkgname%-git}"/desktop
    cargo build --release
}

package() {
    cd "${pkgname%-git}"
    install -Dm755 "target/release/ruffle_desktop" "$pkgdir/usr/bin/${pkgname%-git}"
    install -Dm644 README.md -t "$pkgdir/usr/share/doc/$pkgname/"
    install -Dm644 LICENSE.md -t "$pkgdir/usr/share/licenses/$pkgname/"
}
