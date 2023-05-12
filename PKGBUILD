# Maintainer: rydesun <rydesun@gmail.com>

pkgname=ttf-iosevka-custom
pkgver=22.1.1
pkgrel=1
pkgdesc='Typeface family designed for coding, terminal use and technical documents.'
arch=('any')
groups=("custom")
license=('OFL')
url='https://typeof.net/Iosevka/'
makedepends=('nodejs>=14.0.0' 'ttfautohint' 'npm' 'git')
source=('private-build-plans.toml')
sha256sums=('SKIP')

prepare() {
  if test -e "$pkgname-$pkgver"; then
    rm -rf "$pkgname-$pkgver"
  fi
  # Should shallow clone
  git clone --branch v$pkgver --depth 1 \
    https://github.com/be5invis/Iosevka.git "$pkgname-$pkgver"
}

build() {
  cd "$pkgname-$pkgver"
  cp $srcdir/private-build-plans.toml .
  npm install
  npm run build -- ttf::iosevka-custom
}

package() {
  cd "$pkgname-$pkgver"
  install -d "$pkgdir/usr/share/fonts/iosevka-custom/"
  install -Dm644 dist/iosevka-custom/ttf/*.ttf "$pkgdir/usr/share/fonts/iosevka-custom/"
  install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
