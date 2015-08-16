# Maintainer: Lara Maia <lara@craft.net.br>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>
# Contributor: josephgbr <rafael.f.f1 at gmail dot com>

pkgname=lib32-glew1.5
pkgver=1.5.8
pkgrel=4
pkgdesc="Legacy version of the OpenGL Extension Wrangler Library (32 bit)"
arch=(x86_64)
url='http://sourceforge.net/projects/glew'
license=(BSD MIT GPL)
options=(strip)
depends=(glew1.5 lib32-libxi lib32-libxmu lib32-mesa)
makedepends=(gcc-multilib)
source=(http://downloads.sourceforge.net/glew/glew-$pkgver.tgz)
md5sums=('342c8dc64fb9daa6af245b132e086bdd')

prepare() {
	cd "$srcdir"/glew-$pkgver/
	
	sed -i 's|CC = cc|CC = gcc -m32|g' config/Makefile.linux
    sed -i 's|LD = cc|LD = gcc -m32|g' config/Makefile.linux
    sed -i 's|lib64|lib32|g' config/Makefile.linux
    
    make clean
}

build() {
    cd "$srcdir"/glew-$pkgver/
    
	make
}

package() {
    cd "$srcdir"/glew-$pkgver/

    # We want only these two libraries
    strip -x lib/libGLEW.so.$pkgver
    install -Dm644 lib/libGLEW.so.$pkgver "$pkgdir"/usr/lib32/libGLEW.so.$pkgver
    ln -sf libGLEW.so.$pkgver "$pkgdir"/usr/lib32/libGLEW.so.1.5
    chmod 755 "$pkgdir"/usr/lib32/libGLEW.so.$pkgver

    # License
    mkdir -p "$pkgdir"/usr/share/licenses
    ln -s glew1.5 "$pkgdir"/usr/share/licenses/$pkgname
}
