# Maintainer: Xentec <xentec at aix0 dot eu>

_name=globjects
pkgname=${_name}-git
pkgver=1.1.0.r148.g6e3f2d54
pkgrel=1
pkgdesc="A generated C++ binding for the OpenGL API, generated using the gl.xml specification"
arch=('i686' 'x86_64')
url="http://www.glbinding.org/"
license=('MIT')

depends=('glfw' 'glm' 'glbinding-git')
makedepends=('cmake' 'git')

source=("$pkgname"::'git+https://github.com/cginternals/globjects.git')
sha256sums=('SKIP')

pkgver() {
	cd "$pkgname"
	git describe --long --tags | sed -r 's/([^-]*-g)/r\1/;s/-/./g;s/^v//'
}

prepare() {
	sed 's/glm::glm/glm/' $srcdir/$pkgname/source/globjects/CMakeLists.txt > $srcdir/$pkgname/source/globjects/CMakeLists.txt
}


build() {
	mkdir -p build && cd build
	cmake -Wno-dev \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_BUILD_TYPE=Release \
		-DOPTION_BUILD_TESTS=0 \
		"../$pkgname"

	make
}

package() {
	export DESTDIR="$pkgdir"
	make -C build install
	cp -r $srcdir/$pkgname/source/globjects/include/globjects $pkgdir/usr/include
}

