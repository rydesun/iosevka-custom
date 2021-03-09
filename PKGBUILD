# Maintainer: rydesun <rydesun@gmail.com>

pkgname=ttf-iosevka-custom
pkgver=5.0.5
pkgrel=1
pkgdesc='Typeface family designed for coding, terminal use and technical documents.'
arch=('any')
groups=("custom")
license=('custom')
url='https://github.com/be5invis/Iosevka'
makedepends=('ttfautohint' 'otfcc' 'python-pip' 'npm' 'git')
source=('private-build-plans.toml')
sha256sums=('SKIP')

prepare() {
  if test -e "$pkgname-$pkgver"; then
    rm -rf "$pkgname-$pkgver"
  fi
  # Should shallow clone
  git clone --branch v$pkgver --recursive --depth 1 \
    https://github.com/be5invis/Iosevka.git "$pkgname-$pkgver"
}

build() {
  # Setup pyvenv
  python3 -m venv $srcdir/pyvenv
  source $srcdir/pyvenv/bin/activate
  pip3 install afdko

  cd "$pkgname-$pkgver"
  cp $srcdir/private-build-plans.toml .
  npm install
  npm run build -- ttf::custom
}

package() {
  cd "$pkgname-$pkgver"
  mkdir -p "$pkgdir/usr/share/fonts/iosevka-custom"
  install -Dm644 dist/custom/ttf/*.ttf "$pkgdir/usr/share/fonts/iosevka-custom"
}
