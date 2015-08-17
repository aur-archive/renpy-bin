# Contributor: Eric Forgeot < http://ifiction.free.fr > & franzrogar
# Maintainer: Ben R <thebenj88 *AT* gmail *DOT* com>

pkgname=renpy-bin
_realname=renpy
pkgver=6.18.1
pkgrel=1
pkgdesc="A free and cross-platform engine that helps you use words, pictures, and sounds to tell stories with the computer."
arch=(x86_64 i686)
url="http://www.renpy.org"
license=(MIT)
depends=(bash ffmpeg-compat glu hicolor-icon-theme python2 sdl_image)
makedepends=(imagemagick)
conflicts=(renpy)
install=$pkgname.install
options=(!strip)
source=(http://www.renpy.org/dl/$pkgver/renpy-$pkgver-sdk.tar.bz2
		renpy.launcher
		$pkgname.desktop)

sha256sums=('bc87d7b3b51a35774d85a8ff2976718802003d4c303435475bb97731bead6a52'
            'b28db62765e2662aa7869decea89d69ab26b6dda689978edeb038317a796cc56'
            '40573814c7499df2915971b751bb40a56190854d0b709fe52db87aec486a935c')

prepare()
{
	[[ $CARCH == x86_64 ]] && rm -rf "$srcdir/${_realname}-${pkgver}-sdk/lib/linux-i686"
	[[ $CARCH == i686 ]] && rm -rf "$srcdir/${_realname}-${pkgver}-sdk/lib/linux-x86_64"
	rm "$srcdir/${_realname}-${pkgver}-sdk/renpy.exe"
	convert "$srcdir/${_realname}-${pkgver}-sdk/the_question/icon.ico" "$srcdir/renpy.png"
}



package() {
    cd "$srcdir/${_realname}-${pkgver}-sdk"

	mkdir -p "$pkgdir/usr/share/renpy"

	cp -r "$srcdir"/${_realname}-${pkgver}-sdk/* "$pkgdir/usr/share/renpy"

	install -Dm755 "$srcdir/renpy.launcher" "$pkgdir/usr/bin/renpy"

	# desktop icons
	count=0
    for size in 256x256 48x48 32x32 16x16
	do
		install -Dm644 "$srcdir/renpy-${count}.png" \
			"$pkgdir/usr/share/icons/hicolor/${size}/renpy.png"
		count=$((count + 1))
	done
	install -Dm644 "$srcdir/renpy-bin.desktop" "$pkgdir/usr/share/applications/renpy.desktop"
	install -Dm644 "$srcdir/${_realname}-${pkgver}-sdk/LICENSE.txt" \
		"$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
