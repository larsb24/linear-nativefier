pkgname=linear-nativefier
pkgver=1.0
pkgrel=1
pkgdesc="Linear.app made with nodejs-nativefier (electron)"
arch=("i686" "x86_64")
url="https://linear.app/"
license=("GPL")
depends=("gtk3" "libxss" "nss")
optdepends=("libindicator-gtk3")
makedepends=("imagemagick" "nodejs-nativefier")

source=("${pkgname}.desktop" "${pkgname}.png")
sha256sums=("b65dd9f7afe69e497c78a21ab74c583eb5edf90490201ec2b9060c2e12516ab7"
            "83259e592be46546143e2286e77e5141917597fb3f0722e7be87212fa1260496")

build() {
	cd "${srcdir}"
	nativefier "https://linear.app" --name "Linear" --internal-urls ".*linear.app.*" -m -i "${pkgname}.png"
}

package() {
	install -dm755 "${pkgdir}/"{opt,usr/share/applications,usr/bin}
	cp -rL "${srcdir}/Linear-linux"* "${pkgdir}/opt/${pkgname}"
	chmod +x "${pkgdir}/opt/${pkgname}/Linear"
	ln -s "/opt/${pkgname}/Linear" "${pkgdir}/usr/bin/${pkgname}"
	install -Dm644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
	for _size in "192x192" "128x128" "96x96" "64x64" "48x48" "32x32" "24x24" "22x22" "20x20" "16x16" "8x8"
	do
		install -dm755 "${pkgdir}/usr/share/icons/hicolor/${_size}/apps"
		convert "${srcdir}/${pkgname}.png" -resize "${_size}" "${pkgdir}/usr/share/icons/hicolor/${_size}/apps/${pkgname}.png"
	done
}
