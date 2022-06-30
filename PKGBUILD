# Maintainer: Bernhard Landauer <oberon@manjaro.org>
# Contributor: Chrysostomus @forum.manjaro.org
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Thorsten Töpper <atsutane-tu@freethoughts.de>
# Contributor: Thayer Williams <thayer@archlinux.org>
# Contributor: Jeff 'codemac' Mickey <jeff@archlinux.org>
# Contributor: Jonathon Fernyhough <jonathon at manjaro_dot_org>
# Contributor: Indian Sunset @idnsusnet
# Contributor: Karthik Chikmagalur

pkgname=dmenu-manjaro
_pkgname=dmenu
pkgver=r7.02c053a
pkgrel=1
pkgdesc="customized recency-aware dmenu for manjaro-i3 with xft- and mouse-support"
arch=('x86_64' 'aarch64')
groups=('i3-manjaro')
license=('MIT')
depends=('coreutils'
         'fontconfig'
         'freetype2'
         'glibc'
         'libfontconfig.so'
         'libx11'
         'libxinerama'
         'libxft'
         'libxinerama'
         'noto-fonts'
         'sh')
conflicts=("$_pkgname" "$_pkgname-xft")
provides=("$_pkgname" "$_pkgname-xft")
source=("${_pkgname}::git+https://github.com/karthink/dmenu.git#branch=extras")
md5sums=('SKIP')
sha1sums=('SKIP')

pkgver() {
	cd "$srcdir/${_pkgname}"
# Git, tags available
	# printf "%s" "$(git describe --tags | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"

# Git, no tags available
        printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
    cd $_pkgname
    echo "CPPFLAGS+=${CPPFLAGS}" >> config.mk
    echo "CFLAGS+=${CFLAGS}" >> config.mk
    echo "LDFLAGS+=${LDFLAGS}" >> config.mk
}

build() {
	cd $_pkgname
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
	cd $_pkgname
	make PREFIX=/usr DESTDIR="$pkgdir" install
	install -Dm755 "$srcdir/${_pkgname}/dmenu_recency" "$pkgdir/usr/bin/dmenu_recency"
	install -Dm755 "$srcdir/${_pkgname}/dmenurc" "$pkgdir/usr/share/$_pkgname/dmenurc"
        install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

post_install() {
  echo ""
  echo ">>> Font, colour and your preferred terminal application for dmenu"
  echo "    can be set in ~/.dmenurc"
  echo ""
}

post_upgrade() {
  echo ""
  echo ">>> dmenu can be configured in your ~/.dmenurc file."
  echo "    To change your preferred terminal command edit or add the variable 'TERMINAL_CMD'"
  echo "    for example: TERMINAL_CMD=\"lxterminal -e\""
  echo ""
}
