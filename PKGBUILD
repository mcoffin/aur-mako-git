# Maintainer: Drew DeVault <sir@cmpwn.com>
pkgname=mako-git
_pkgname=mako
pkgver=1.4.1.r0.ad97299
pkgrel=1
license=('MIT')
pkgdesc='Lightweight notification daemon for Wayland'
makedepends=("meson" "scdoc" "wayland-protocols" "git")
depends=(
	"pango"
	"cairo"
	"wayland"
)
optdepends=("jq: support for 'makoctl menu'")
arch=("x86_64")
url='http://mako-project.org'
source=("${pkgname%-*}::git+git://github.com/emersion/mako.git?signed#tag=v1.4.1")
sha256sums=('SKIP')
validpgpkeys=(
	'34FF9526CFEF0E97A340E2E40FDE7BE0E88F5E48' # Simon "emersion" Ser
)
provides=('mako')
conflicts=('mako')

pkgver() {
	cd "$_pkgname"
	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g' | sed -E 's/^v//g')"
}

build() {
	cd "$_pkgname"
	meson \
		--prefix /usr \
		--buildtype release \
		. build
	ninja -C build
}

package() {
	cd "$_pkgname"
	DESTDIR="$pkgdir/" ninja -C build install
	install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/"${pkgname%-*}"/LICENSE
}
