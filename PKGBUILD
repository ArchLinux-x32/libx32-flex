# Maintainer: Bill Fraser <wfraser@codewise.org>
#
# From flex's PKGBUILD:
#   Maintainer: Allan McRae <allan@archlinux.org>
#   Contributor: judd <jvinet@zeroflux.org>

_pkgbasename=flex
pkgname=lib32-flex
pkgver=2.5.35
pkgrel=4
pkgdesc="A tool for generating text-scanning programs"
arch=('x86_64')
url="http://flex.sourceforge.net"
license=('custom')
groups=('base-devel')
depends=('lib32-glibc' 'm4' 'sh' $_pkgbasename)
source=(http://downloads.sourceforge.net/sourceforge/flex/flex-$pkgver.tar.bz2 
        flex-2.5.35-gcc44.patch
        flex-2.5.35-hardening.patch
        flex-2.5.35-missing-prototypes.patch
        flex-2.5.35-sign.patch
        lex.sh)
md5sums=('10714e50cea54dc7a227e3eddcd44d57'
         'e4444ef5c07db71a43280be74139bdea'
         'de952b3ed7cc074bc8c3e6ab73634048'
         '6b83f56b1b654c6a321cdc530a3ec68d'
         'd87fd9e9762ba7e230d516bdcf1c8c6f'
         'f725259ec23a9e87ee29e2ef82eda9a5')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export LD="ld -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd $srcdir/$_pkgbasename-$pkgver

  patch -Np1 -i $srcdir/flex-2.5.35-gcc44.patch
  patch -Np1 -i $srcdir/flex-2.5.35-hardening.patch
  patch -Np1 -i $srcdir/flex-2.5.35-missing-prototypes.patch
  patch -Np1 -i $srcdir/flex-2.5.35-sign.patch

  ./configure --prefix=/usr --libdir=/usr/lib32 \
    --mandir=/usr/share/man --infodir=/usr/share/info
  make
}

check() {
  cd $srcdir/$_pkgbasename-$pkgver
  make check
}

package() {
  cd $srcdir/$_pkgbasename-$pkgver

  make prefix=$pkgdir/usr \
    mandir=$pkgdir/usr/share/man \
    infodir=$pkgdir/usr/share/info \
    libdir=$pkgdir/usr/lib32 \
    install

  rm -rf "${pkgdir}"/usr/{include,share,bin}

  mkdir -p $pkgdir/usr/share/licenses
  ln -s $_pkgbasename "$pkgdir/usr/share/licenses/$pkgname"
}

