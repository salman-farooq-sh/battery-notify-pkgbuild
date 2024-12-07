# Maintainer: dadav <dadav at protonmail dot com>

pkgname=battery-notify-salman
pkgver=0.3.5.r5.g6fe268d
pkgrel=1
pkgdesc='A simple battery notifier for Linux.'
arch=('x86_64')
url='https://github.com/cdown/battery-notify'
license=('MIT')
makedepends=('git' 'cargo')
provides=("battery-notify-salman=$pkgver")
conflicts=("battery-notify" "battery-notify-git")
source=("$pkgname::git+$url")
sha256sums=('SKIP')

pkgver() {
  git -C "$pkgname" describe --long --tags | sed 's/v//g;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$pkgname"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target

  cd "$pkgname"
  cargo build --release --frozen --no-default-features
}

check() {
  export RUSTUP_TOOLCHAIN=stable

  cd "$pkgname"
  cargo test --frozen --no-default-features
}

package() {
  cd "$pkgname"
  install -Dm755 battery-notify.service -t "$pkgdir/usr/lib/systemd/user/"
  install -D target/release/battery-notify -t "$pkgdir/usr/bin/"
  install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
}

# vim:set ts=2 sw=2 et:
