# Maintainer :  minego 
# Contributor: minego <m@minego.net>
pkgname='slack-nativefier'
pkgver=1.0.0
pkgrel=1
pkgdesc="A native-like OS X, Windows, & Linux desktop app for Slack"
arch=('x86_64' 'i686' 'pentium4' 'armv7h' 'aarch64')
url="https://slack.com/signin#/signin"
license=('custom')
makedepends=('nodejs-nativefier')
source=("slack.desktop")
sha256sums=('0735d75a4f8acf7b4baf77e8993f5ea00d29a40b582c502bae11e3e150963742')

build() {
	if [ "$CARCH" = "x86_64" ]; then
	    _NFARCH='x64'
	elif [ "$CARCH" = "i686" ] || [ "$CARCH" = "pentium4" ]; then
	    _NFARCH='ia32'
	elif [ "$CARCH" = "aarch64" ]; then
	    _NFARCH='arm64'
	elif [ "$CARCH" = "armv7h" ]; then
	    _NFARCH='armv7l'
	else
	    echo "Unsupported architecture. Aborting"
	    exit 1
	fi
	nativefier --platform "linux" --name "Slack" "https://venafi.slack.com/" --honest --disable-dev-tools --single-instance --app-version $pkgver --build-version $pkgrel --arch ${_NFARCH}
}

package() {
	_INSTDIR=$(ls -l "${srcdir}" | grep "Slack-linux-" | awk '{print $9}')
	mkdir -p "$pkgdir"/opt
	mv ${_INSTDIR} "$pkgdir"/opt/slack
	mkdir -p "$pkgdir"/usr/bin
	ln -s /opt/slack/Slack "$pkgdir"/usr/bin/slack
	install -Dm644 slack.desktop "$pkgdir"/usr/share/applications/slack.desktop
}
