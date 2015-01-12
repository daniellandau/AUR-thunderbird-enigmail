# Maintainer: Daniel Landau <daniel.landau@iki.fi>
# Contributor: Xyne
# Contributor: David Manouchehri <d@32t.ca>
# Contributor: Alexander Fehr <pizzapunk gmail com>
# Contributor: Thomas Jost <schnouki schnouki net>
# Contributor: Hinrich Harms <arch hinrich de>

# the PKGBUILD lives in https://github.com/daniellandau/AUR-thunderbird-enigmail
# pull requests are welcome

pkgname=thunderbird-enigmail
pkgver=1.7.2
pkgrel=2
pkgdesc="Thunderbird extension that enables sending and receiving signed and encrypted e-mail messages"
arch=('i686' 'x86_64')
url="https://www.enigmail.net/"
license=('MPL' 'GPL')
depends=('thunderbird' 'gnupg')
makedepends=('zip' 'unzip' 'python2' 'perl>=5.8')
source=("https://www.enigmail.net/download/source/enigmail-${pkgver}.tar.gz"{,.asc}) # gpg --recv-keys 9369CDF3
validpgpkeys=('10B2E4A0E718BB1B2791DAC4F040E41B9369CDF3')
sha256sums=('7b3a62e83961bafec1cdac60075aa6c317c8f655a837e31a7d1f3ce6a49fc7d6'
            'SKIP')

build() {
  cd "$srcdir/enigmail"
  PYTHON=/usr/bin/python2 ./configure
  make -j1 # fails with -j greater than 1
}

package() {
  cd "$srcdir/enigmail"
  emid="$(sed -n '/.*<em:id>\(.*\)<\/em:id>.*/{s//\1/p;q}' package/install.rdf)"
  install -d -m755 "$pkgdir"/usr/lib/thunderbird/extensions/"$emid"
  cd "$pkgdir"/usr/lib/thunderbird/extensions/"$emid"
  unzip "$srcdir"/enigmail/build/enigmail-*.xpi

  # Uncomment the following lines if you use thunderbird-nightly
  # install -d -m755 "$pkgdir"/opt/thunderbird-nightly-*/extensions/"$emid"
  # cd "$pkgdir"/opt/thunderbird-nightly-*/extensions/"$emid"
  # unzip "$srcdir"/enigmail/build/enigmail-*.xpi
}
