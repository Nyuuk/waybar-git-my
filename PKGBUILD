# Maintainer: Alexis Rouillard <contact@arouillard.fr>

pkgname=waybar-git
pkgver=r636.67593b8
pkgrel=1
pkgdesc='Highly customizable Wayland bar for Sway and Wlroots based compositors (GIT)'
arch=('x86_64')
url='https://github.com/Alexays/Waybar/'
license=('MIT')
provides=('waybar')
conflicts=('waybar')
depends=('gtkmm3'
         'fmt'
         'jsoncpp'
         'libinput'
         'libnl>=3.0'
         'libsigc++>=2.0'
         'wayland'
         'libdbusmenu-gtk3'
         'libappindicator-gtk3'
         'libpulse')
makedepends=('meson'
             'git')
optdepends=('sway: Sway modules support'
            'libmpdclient: Mpd module support'
            'otf-font-awesome: Icons in the default configuration')

source=("${pkgname}::git://github.com/Alexays/Waybar"
        'meson.build.patch')

sha1sums=('SKIP'
          'f4984a4a4044bd04bebee584d5e5801d0ae31760')

pkgver() {
    cd "${srcdir}/${pkgname}"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

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
