# Maintainer: BL4CKH47H4CK3R <109698175+BL4CKH47H4CK3R@users.noreply.github.com>

pkgname=Hardened-Anonymized-DNSCrypt-Proxy
_pkgname=dnscrypt-proxy
pkgver=2.1.5.r38.g658835b4
pkgrel=1
pkgdesc="Wipe Snoopers Out Of Your Networks"
arch=('x86_64' 'x86_64_v3')
url="https://github.com/BL4CKH47H4CK3R/Hardened-Anonymized-DNSCrypt-Proxy"
license=(ISC)
depends=(glibc)
makedepends=(git go)
optdepends=('python-urllib3: for generate-domains-blocklist')
provides=(dnscrypt-proxy)
conflicts=(dnscrypt-proxy)
install=$_pkgname.install
# NOTE: LTO breaks reproducibility :(
options=(!lto)
source=(
	git+https://github.com/dnscrypt/$_pkgname.git
	$_pkgname.toml
	$_pkgname.service
)
sha512sums=('SKIP'
            '637b081b7fc7afcea5659d5a2d339745986feef6e7cae358349caaf75a65f9eaa531a94b5af2ad98511c072e764877d5b98c9b4b454c74e7a8860a89b8437f0d'
            '50e6c878115c96e72f6118008e92871957a699d89bd0b85c80af45e6880a30b0832995e4718ab585b086049cc64e2b0759f8f4263ef814d74929933534403f92')

pkgver() {
	cd "$_pkgname"
	git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cd $_pkgname/$_pkgname
	export CGO_CPPFLAGS="$CPPFLAGS"
	export CGO_CFLAGS="$CFLAGS"
	export CGO_CXXFLAGS="$CXXFLAGS"
	export CGO_LDFLAGS="$LDFLAGS"
	export GOPATH="$srcdir"
	export GOFLAGS="-buildmode=pie -mod=readonly -modcacherw"

	go build -ldflags "-compressdwarf=false -linkmode external" .
}

package() {
	local _config
	cd $_pkgname
	# executable
	install -Dm 755 $_pkgname/$_pkgname -t "$pkgdir/usr/bin/"
	# config files
	install -Dm 644 ../$_pkgname.toml "$pkgdir/etc/$_pkgname/$_pkgname.toml"
	for _config in {{allowed,blocked}-{ips,names},{cloaking,forwarding}-rules,captive-portals}.txt; do
		install -Dm 644 $_pkgname/example-$_config "$pkgdir/etc/$_pkgname/$_config"
	done
	# utils
	install -Dm 644 utils/generate-domains-blocklist/*.{conf,txt} -t "$pkgdir/usr/share/$_pkgname/utils/generate-domains-blocklist"
	install -Dm 755 utils/generate-domains-blocklist/generate-domains-blocklist.py "$pkgdir/usr/bin/generate-domains-blocklist"
	# systemd service
	install -Dm 644 ../$_pkgname.service -t "$pkgdir/usr/lib/systemd/system/"
	# license
	install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$_pkgname"
	# docs
	install -Dm 644 {ChangeLog,README.md} -t "$pkgdir/usr/share/doc/$_pkgname"
}
# vim:set ts=2 sw=2 et:
