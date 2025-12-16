# Maintainer: Alexandru Iercosan-Lucaci <lucaci32u4@gmail.com>

#
# $ makepkg -si
#
# Set WONDERDRAFT_DOWNLOAD_URL with the download url provided by
# the Humble Bundle purchase page and the nrun makepkg.
#
# It will work with all current versions of Wonderdraft.
# The version string is detected dinamically when run.
#

WONDERDRAFT_DOWNLOAD_URL='https://cdn.humble.com/humblebundle/tailwindgamesllc_ChunI/Wonderdraft-1.1.8.2-b-Linux64.zip?gamekey=insert_your_gamekey here'

pkgname=wonderdraft
pkgrel=4

pkgdesc='Wonderdraft is a tabletop encounter map creation tool designed to draw aesthetic maps without the typical frustrations and time investment'

arch=('x86_64')
url='https://wonderdraft.net'
license=('custom:TailwindGamesLicense')

depends=('mono' 'zenity')
makedepends=('unzip')

red_color='\033[0;31m'
yellow_color='\033[0;33m'
bold_font='\033[1m'
no_color='\033[0m'



if [[ -z $WONDERDRAFT_DOWNLOAD_URL ]]; then
	echo -e "${red_color}${bold_font}==> ERROR:${no_color}${bold_font} You need to set WONDERDRAFT_DOWNLOAD_URL to install Wonderdraft!"
	echo ""
	echo "To get the download URL go to your Humble Bundle purchases https://www.humblebundle.com/home/purchases, select Wonderdraft and then copy the link from the \"Manual Install\" button under the Linux section."
	echo "Afterwards execute \"export WONDERDRAFT_DOWNLOAD_URL=<the url you copied>\"."
	exit 12
fi

if [[ ! $WONDERDRAFT_DOWNLOAD_URL =~ ^https://cdn.humble.com/humblebundle/tailwindgamesllc_ChunI/Wonderdraft.* ]]; then
	echo -e "${red_color}${bold_font}==> ERROR:${no_color}${bold_font} WONDERDRAFT_DOWNLOAD_URL seems to be invalid! Your download link has to start with \"https://cdn.humble.com/humblebundle/tailwindgamesllc_ChunI/Wonderdraft*\"."
	exit 12
fi
# # #
if [[ ! $WONDERDRAFT_DOWNLOAD_URL =~ ^https://cdn.humble.com/humblebundle/tailwindgamesllc_ChunI/Wonderdraft.*-Linux64\.zip.* ]]; then
	echo -e "${red_color}${bold_font}==> ERROR:${no_color}${bold_font} WONDERDRAFT_DOWNLOAD_URL seems to be invalid! You must select the \"Manual Install\", not the .deb package!"
	exit 12
fi

source=("$WONDERDRAFT_DOWNLOAD_URL")
pkgver="$(echo "$WONDERDRAFT_DOWNLOAD_URL" | grep -oE '[0-9]+(\.[0-9]+)*' | head -n 1)"
if [[ "$pkgver" == "1.1.0.6" ]]; then
	md5sums=('11c548c3c9ad238a0e96fef11d64b26f')
elif [[ "$pkgver" == "1.2.0.1" ]]; then
	md5sums=('cf1f66ca9b2d6c7eb00567702a379b41')
elif [[ "$pkgver" == "1.0.3.2" ]]; then
	md5sums=('3f6ceb8096fca8fd48fb6f1438b21236')
else
	echo -e "${yellow_color}${bold_font}==> WARNING:${no_color}${bold_font} No md5sum for v$pkgver found, cannot validate your download!"
	md5sums=('SKIP')
fi

package() {
	local destdir="$pkgdir/opt/Wonderdraft"
	install -d "$destdir"
	install -d "$pkgdir/usr/share/applications"

	if [ -d "data_Wonderdraft" ]; then
		cp -a "data_Wonderdraft" "$destdir/"
	fi
	if [ -d "translations" ]; then
		cp -a "translations" "$destdir/"
	fi
	if [ -d "mods" ]; then
		cp -a "mods" "$destdir/"
	fi

	install -m 0644 "Wonderdraft.pck" "$destdir/"
	install -m 0644 "Wonderdraft.png" "$destdir/"
	install -m 0644 "EULA.txt" "$destdir/"
	install -m 0644 "Wonderdraft.desktop" "$pkgdir/usr/share/applications/"

	install -m 0755 "Wonderdraft.x86_64" "$destdir/"
}
