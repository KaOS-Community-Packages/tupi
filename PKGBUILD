pkgname=tupi
pkgver=0.2.70
pkgrel=1
_commit=dcd31b64ba571c67e9cbbcdc0f7ca195423057c7
pkgdesc="A design and authoring tool for 2D animation based on ktoon"
url="https://github.com/xtingray/tupi"
license=('GPL')
arch=('x86_64')
depends=(
    'ruby' 'zlib' 'libgl' 'quazip' 'ffmpeg'
    'qt5-base' 'qt5-multimedia' 'qt5-svg' 'qt5-tools'
    'shared-mime-info'
)
source=(
    "tupi.zip::https://github.com/xtingray/tupi/archive/{$_commit}.zip"
    'kaos.patch'
)
md5sums=(
    'f26ad00932e51d24854a8b5ead73b624'
    '7996e02d62df28f8480f4eef0ef982f1'
)

prepare() {
    cd "${srcdir}/tupi-${_commit}"
    patch -p1 -i "${srcdir}/kaos.patch"
    if [ ! -e /usr/bin/qmake ] && [ -e /usr/lib/qt5/bin/qmake ]; then
        export PATH=$PATH:/usr/lib/qt5/bin
    fi
}

build() {
    cd "${srcdir}/tupi-${_commit}"
    ./configure --prefix="/usr" --libdir="/usr/lib" --without-debug
    make
}

package() {
    cd "${srcdir}/tupi-${_commit}"
    make DESTDIR="${pkgdir}/" install

    mkdir -p "${pkgdir}/etc/ld.so.conf.d"
    echo "/usr/lib/tupi" > "${pkgdir}/etc/ld.so.conf.d/tupi.conf"
    echo "/usr/lib/tupi/plugins" >> "${pkgdir}/etc/ld.so.conf.d/tupi.conf"
}
