# Contributor: intelfx <intelfx100 [at] gmail [dot] com>
# Maintainer: Behem0th <grantipak@gmail.com>

#_use_chrome=yes

pkgname=freshplayerplugin-git
_realname=freshplayerplugin
pkgver=20140630
pkgrel=1
pkgdesc='PPAPI-host NPAPI-plugin adapter.'
arch=('i686' 'x86_64')
url='https://github.com/i-rinat/freshplayerplugin'
license=('MIT')
depends=('chromium-pepper-flash' 'pango' 'alsa-lib' 'freetype2' 'uriparser' 'libconfig' 'libevent' 'gtk2' 'libgl')
  if [[ -n $_use_chrome ]]; then
    depends[0]='google-chrome'
  fi
makedepends=('git' 'cmake')
provides=('freshplayerplugin')
conflicts=('freshplayerplugin')
source=('git://github.com/i-rinat/freshplayerplugin.git')
backup=('etc/freshwrapper.conf')
md5sums=('SKIP')
options=(debug !strip)

pkgver() {
  cd "$srcdir/$_realname"
  git log -1 --format="%cd" --date=short | tr -d -
}

build() {
  cd "$srcdir/$_realname"
  cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr
  make
}

package() {
  cd "$srcdir/$_realname"
  install -d "$pkgdir/usr/lib/mozilla/plugins"
  install -m644 libfreshwrapper-*.so "$pkgdir/usr/lib/mozilla/plugins"
  install -Dm644 data/freshwrapper.conf.example "$pkgdir/etc/freshwrapper.conf"
    if [[ ! -n $_use_chrome ]]; then
      # configure path to libpepflashplayer.so
      sed -r -e 's|^(plugin_path).*|\1 = "/usr/lib/PepperFlash/libpepflashplayer.so"|' \
             -i "$pkgdir/etc/freshwrapper.conf"
    fi
}
