# Maintainer: Viacheslav Chimishuk <voice@root.ua>
# Contributors: Nathan Mudie <nathan.mudie@gmail.com>
_pkgname=haproxy
pkgname=$_pkgname-devel
pkgver=1.6
pkgverdev=dev0
pkgrel=1
pkgdesc="The Reliable, High Performance TCP/HTTP Load Balancer (development branch)"
arch=('i686' 'x86_64')
url="http://haproxy.1wt.eu"
license=('GPL')
depends=('pcre' 'openssl' 'zlib')
makedepends=('gcc>=4.2.0')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
backup=('etc/haproxy/haproxy.cfg')
install=$_pkgname.install
source=("http://haproxy.1wt.eu/download/1.6/src/devel/$_pkgname-$pkgver-$pkgverdev.tar.gz")
md5sums=('eb5026b8ae3529fe7201f52896523f67')

build() {
        cd "$srcdir/$_pkgname-$pkgver-$pkgverdev"
        
        make PREFIX=/usr TARGET=linux2628 CPU=native USE_PCRE=1 USE_OPENSSL=1 USE_ZLIB=1

        make -C contrib/systemd PREFIX=/usr
}

package() {
        cd "$srcdir/$_pkgname-$pkgver-$pkgverdev"

        make PREFIX=/usr DESTDIR="$pkgdir" install

        install -D -m644 examples/haproxy.cfg $pkgdir/etc/haproxy/haproxy.cfg
        install -D -m644 contrib/systemd/haproxy.service $pkgdir/lib/systemd/system/haproxy.service
}
