# Maintainer: Whitney Marshall <whitney.marshall@gmail.com>
pkgname=cloudcity-svn
pkgver=1436
pkgrel=1
pkgdesc="A native style for Qt/KDE4"
arch=('i686' 'x86_64')
url="http://cloudcity.sourceforge.net"
license=('LGPL')
depends=('kdebase-workspace>=4')
makedepends=('subversion')
conflicts=('cloudcity')

_svntrunk=https://cloudcity.svn.sourceforge.net/svnroot/cloudcity
_svnmod=cloudcity

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD HERE
  #
  cmake -DCMAKE_INSTALL_PREFIX=$(kde4-config --prefix) -DCMAKE_BUILD_TYPE=Release ../$_svnmod
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
