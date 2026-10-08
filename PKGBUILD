# Maintainer: Rasmus Moorats <xx+aur@nns.ee>
# Maintainer: freb

pkgname=burpsuite-pro
_up_pkg=burpsuite-pro
pkgver=2026.9
pkgrel=1
pkgdesc='An integrated platform for performing security testing of web applications (professional edition)'
url='https://portswigger.net/burp/'
depends=('java-runtime>=21' 'hicolor-icon-theme')
makedepends=('zip')
arch=('any')
license=('custom')
noextract=("${pkgname}-${pkgver}-orig.jar")
source=("${pkgname}-${pkgver}-orig.jar::https://portswigger.net/burp/releases/download?product=desktop&version=${pkgver}&type=Jar"
  "${pkgname}"
  "${pkgname}.desktop"
  'icon16.png'
  'icon24.png'
  'icon32.png'
  'icon48.png'
  'icon128.png'
  'icon256.png'
  'icon512.png'
  'icon.svg'
  'burpsuite-pro-cn-loader.jar')
sha256sums=('d6c80be60575b59a3097e939b1cf4acf2efd104c0f6ed05166753180365fc7fc'
            'e5497af16b54dfe66c195d9dd91ace330888c35578f6f28a8888e12c4094fee7'
            'f442258c5616969bfaad7c20b2ff99f05696ad04c2e2c3d145a360615650b9ec'
            'ff0b230af06fb76af053090ac021bf45b88341d746e67f6bb9e94ba40957d9d8'
            'a6791fcaee558f6744b4f5a3fc0af2c9ad7ce244033e224c4e4464563ac9b911'
            '48d529f2a045b1179d9cd87ffdeb7fd469d963f7606fd22b7edc665d0515e1d2'
            '2b2407b8ab2ee181bfd64e3ba3e3090a328cbef8f53cce20ba76cffbfb3bc1d1'
            '28d17763c17e010936ad8ed44427d9ce6523510f580aefce52eb7c0f26b48045'
            'da6469f32b0acfcad2057cf0920c128bbbf64bc72ec6a4d5e5ba10d5b8a2d859'
            '6bbfd022aa451efeb439a89527b814ae06f7ce6196f7ad8db276e9ad372a7e32'
            '8777077ed5b1809c8adde4c056a315f8ec8f1b79f4c4c0e60eb3582c4d7ab71d'
            'd2f9de7c6fce5adbeb06c661bc38d5b33be06aae53b91dbc9853b9dc76c428ec')

prepare() {
  cp "${srcdir}/${_up_pkg}-${pkgver}.jar" "${srcdir}/${_up_pkg}-${pkgver}-work.jar" 2>/dev/null || \
  cp "${srcdir}/${_up_pkg}-${pkgver}-orig.jar" "${srcdir}/${_up_pkg}-${pkgver}.jar"
  # remove useless chromium versions
  zip -d "${srcdir}/${_up_pkg}-${pkgver}.jar" 'chromium-macosx*.zip' 'chromium-win*.zip' 2>/dev/null || true
}

package() {
  local sharedir="${pkgdir}/usr/share/${_up_pkg}"

  install -Dm644 "${srcdir}/${_up_pkg}-${pkgver}.jar" "${sharedir}/${_up_pkg}.jar"
  install -Dm644 "${srcdir}/${_up_pkg}.desktop" -t "${pkgdir}/usr/share/applications/"
  install -Dm755 "${srcdir}/${_up_pkg}" "${pkgdir}/usr/bin/${_up_pkg}"
  ln -sf "../${_up_pkg}" "${pkgdir}/usr/bin/${pkgname}"

  install -Dm644 "${srcdir}/burpsuite-pro-cn-loader.jar" "${sharedir}/${_up_pkg}-cn-loader.jar"

  # install icons
  for size in 16 24 32 48 128 256 512; do
    install -Dm644 "${srcdir}/icon${size}.png" "${pkgdir}/usr/share/icons/hicolor/${size}x${size}/apps/burpsuite-pro.png"
  done
  install -Dm644 "${srcdir}/icon.svg" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/burpsuite-pro.svg"

  install -Dm644 "${srcdir}/BurpSuiteCN.LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/BurpSuiteCN.LICENSE"
}
