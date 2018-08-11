# Maintainer: Alexis Rouillard <contact@arouillard.fr>

pkgname=waybar-git
pkgver=r70.8d5b61a9
pkgrel=2
pkgdesc='Highly customizable wayland bar for sway or wlroots based compositor.'
arch=('x86_64')
url='https://github.com/Alexays/Waybar/'
license=('MIT')
depends=('gtkmm3'
         'jsoncpp'
         'libinput'
         'libnl>=3.0'
         'libsigc++>=2.0'
         'wayland'
         'waylandpp'
         'wireless_tools'
         'libpulse'
         'wlroots')
makedepends=('meson')

# source=("${pkgname}::git://github.com/Alexays/Waybar#commit=8d5b61a9"
source=("${pkgname}::git://github.com/Alexays/Waybar"
        'meson.build.patch')

sha1sums=('SKIP'
          '2c20d1b264896312f59c14fab12251a7de18b86e')

prepare() {
    cd "${srcdir}/${pkgname}"
    patch meson.build "${srcdir}/meson.build.patch"
}

build() {
    cd "${srcdir}/${pkgname}"
    rm -rf "${srcdir}/build"
    meson --wrap-mode=nofallback --prefix=/usr "${srcdir}/build"
    ninja -C "${srcdir}/build"
}

package() {
    DESTDIR="$pkgdir" ninja -C "${srcdir}/build" install
}
