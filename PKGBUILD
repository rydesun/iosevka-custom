# Maintainer: rydesun <rydesun@gmail.com>

pkgname=ttf-iosevka-custom
pkgver=3.6.2
pkgrel=1
pkgdesc='Typeface family designed for coding, terminal use and technical documents.'
arch=('any')
license=('custom')
url='https://github.com/be5invis/Iosevka'
makedepends=('ttfautohint' 'otfcc' 'python-pip' 'nvm' 'npm' 'git')
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

  # Setup nodejs 12.16.0
  export NVM_DIR=$srcdir/nvm
  source /usr/share/nvm/init-nvm.sh
  nvm install 12.16.0
  nvm use 12.16.0

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
