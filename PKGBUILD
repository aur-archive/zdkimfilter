# Maintainer: Andrej Podzimek <andrej@podzimek.org>

pkgname=zdkimfilter
pkgver=1.2
_courierver="$(pacman -Q courier-mta)"
_courierver="${_courierver#* }"
_couriernum="${_courierver#*0.}"
_couriernum="${_couriernum%-*}"
_couriernum="${_couriernum%%.*}"
pkgrel=4
pkgdesc='A DKIM filter for the Courier-MTA mail server'
arch=('i686' 'x86_64')
url='http://www.tana.it/sw/zdkimfilter/'
license=('GPLv3')
backup=('etc/courier/filters/zdkimfilter.conf')
depends=('courier-mta='"${_courierver}" 'opendkim' 'opendbx' 'nettle' 'glibc')
makedepends=('pkg-config' 'libtool' 'sed')
source=('http://www.tana.it/sw/zdkimfilter/zdkimfilter-1.2.tar.gz')
sha1sums=('ee8d7a8b200b96b858ab183e7f1daae4f010f340')

build() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	./configure \
		--prefix=/usr \
		--with-courier-version="${_couriernum}"
	make -j
}

package() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	sed -i 's|/usr/lib/filters|'"${pkgdir}"'/usr/lib/filters|;
		s|/etc/courier/filters|'"${pkgdir}"'/etc/courier/filters|' \
		Makefile src/Makefile etc/Makefile tests/Makefile
	make -j prefix="${pkgdir}"/usr install
	chown courier:courier \
		"${pkgdir}"/etc/courier/filters/zdkimfilter.conf{,.dist}
}
