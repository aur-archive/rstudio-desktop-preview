# Maintainer: Meow < a.li.devtty at gmail dot com >

# Get download links and md5 sums for latest version of RStudio desktop
cat <<_EOF_ >/dev/null
## R code #############
require(XML)
page = htmlTreeParse("http://www.rstudio.com/products/rstudio/download/",useInternalNodes = T)
links = sapply(getNodeSet(page,'//table[@class="downloads"]/thead/tr/th[text()="Installers"]/../../..//a[contains(@href,".deb")]'),xmlGetAttr,'href')
md5sums = sapply(getNodeSet(page,'//table[@class="downloads"]/thead/tr/th[text()="Installers"]/../../..//a[contains(@href,".deb")]/../..//code'),xmlValue)
print(cbind(links,md5sums))
#######################
_EOF_

pkgname=rstudio-desktop-preview
pkgver=0.99.441
pkgrel=2
pkgdesc="A new integrated development environment (IDE) for R (binary version from RStudio official website)"
arch=('i686' 'x86_64')
license=('GPL')
url="http://www.rstudio.org/"
depends=('r>=2.11.1' 'qtwebkit' 'shared-mime-info')
conflicts=('rstudio-desktop' 'rstudio-desktop-git' 'rstudio-desktop-preview-bin')
provides=("rstudio-desktop=${pkgver}")
#options=(!strip)



_x86md5=69337bf40062da23b441bbaff6753667
_x86_64md5=6a5dc03fac32df8725c9f57e3608e029
case "$CARCH" in
	'i686')
		_arch=i386
		md5sums=($_x86md5)
		;;
	'x86_64')
		_arch=amd64
		md5sums=($_x86_64md5)
		;;
esac
source=("https://s3.amazonaws.com/rstudio-dailybuilds/rstudio-${pkgver}-${_arch}.deb")
install="$pkgname".install

package() {
  msg "Converting debian package..."
  cd "$srcdir"
  tar zxpf data.tar.gz -C "$pkgdir"
  install -dm755 "$pkgdir/usr/bin"
  cd "$pkgdir/usr/lib/rstudio/bin"
  rm lib*.so.*
  rm -rf plugins qt.conf
  cd "$pkgdir/usr/bin"
  ln -s -f ../lib/rstudio/bin/rstudio rstudio-bin
}
# vim:ft=sh tabstop=2 expandtab
