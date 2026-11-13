# Maintainer: Muflone http://www.muflone.com/contacts/english/
# Contributor: Aelius (find me on Freenode)
# Contributor: callmejoe mrsteve0924@verizon.net
pkgname=gdevilspie
pkgver=0.5
pkgrel=6
pkgdesc="GTK graphical interface for the Devilspie window matching daemon"
arch=('any')
url='https://code.google.com/archive/p/gdevilspie/'
license=('GPL-3.0-or-later')
depends=('python' 'python-gobject' 'gtk3' 'libwnck3' 'python-pyxdg' 'procps-ng' 'devilspie')
source=("https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/${pkgname}/${pkgname}-${pkgver}.tar.bz2" 'python3-gtk3.patch')
sha256sums=('e03ab813e56b6dc6d868db7c318d280c9864cfa6e8a4ca84a5bb5d05542f55ff'
            '305463d425350b50f62a4bfa992d39fedae523bf4a36e5d734dc590c1c288f29')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -Np1 -i "${srcdir}/python3-gtk3.patch"
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  local site_packages
  site_packages=$(python -c 'import sysconfig; print(sysconfig.get_path("purelib", vars={"base": "/usr"}))')

  install -Dm755 gdevilspie "${pkgdir}/usr/bin/gdevilspie"
  install -Dm644 -t "${pkgdir}${site_packages}/gDevilspie" gDevilspie/*.py
  python -m compileall -q -o 0 -o 1 -s "${pkgdir}" -p / "${pkgdir}${site_packages}/gDevilspie"
  install -Dm644 -t "${pkgdir}/usr/share/gdevilspie" gdevilspie.glade gdevilspie.png
  install -Dm644 gdevilspie.desktop "${pkgdir}/usr/share/applications/gdevilspie.desktop"
  install -Dm644 gdevilspie.png "${pkgdir}/usr/share/pixmaps/gdevilspie.png"
  install -Dm644 -t "${pkgdir}/usr/share/doc/gdevilspie" README Changelog TODO
}
