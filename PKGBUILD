# Maintainer: Alex Talker <alextalker at openmailbox dot org>
# Old Maintainer: Tobias Kohlbau <tobias.kohlbau@gmail.com>
pkgname=intellij-idea-12-community
pkgver=12.1.6
_buildver=129.1359
pkgrel=1
pkgdesc='An intelligent IDE for Java, Groovy and other programming languages with advanced refactoring features intensely focused on developer productivity.'
arch=('i686' 'x86_64') # not 'any' because of fsnotifier
url="http://www.jetbrains.com/idea/"
backup=("usr/share/${pkgname}/bin/idea.vmoptions" "usr/share/${pkgname}/bin/idea64.vmoptions")
license=('Apache')
depends=('java-environment' 'giflib')
source=("http://download-ln.jetbrains.com/idea/ideaIC-${pkgver}.tar.gz" \
        "${pkgname}.sh" \
        "${pkgname}.desktop")
md5sums=('5731ad2d6113ea7e8aedffc011480cb8'
         'e64ec59b8dd4ed4dc34f40e57757a760'
         'bf796fdf426739e331b67845be14f54d')

package() {
  cd "${srcdir}"

  install -d -m755 $pkgdir/usr/{bin,share}
  cp -a "idea-IC-${_buildver}" "${pkgdir}/usr/share/${pkgname}"
  chown -R root:root "${pkgdir}/usr/share"
  find $pkgdir/usr/share/$pkgname -type d -exec chmod 0755 {} ';'
  find $pkgdir/usr/share/$pkgname -type f -exec chmod 0644 {} ';'

  # never wait on user input when starting idea; copied from -ce PKGBUILD
  sed -i '/.*read IGNORE.*/ d' "${pkgdir}"/usr/share/$pkgname/bin/idea.sh

  chmod +x $pkgdir/usr/share/$pkgname/bin/idea.sh
  chmod +x "$pkgdir"/usr/share/$pkgname/bin/fsnotifier
  chmod +x "$pkgdir"/usr/share/$pkgname/bin/fsnotifier64

  install -D -m755 "${srcdir}/${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
  install -D -m644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install -D -m644 "$srcdir/idea-IC-$_buildver/bin/idea.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
  install -D -m644 "$srcdir/idea-IC-$_buildver/LICENSE.txt" "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"
}
