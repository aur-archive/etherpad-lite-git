# Maintainer: Thomas Oster <thomas.oster@rwth-aachen.de> 
pkgname=etherpad-lite-git
pkgver=20120515
pkgrel=1
pkgdesc="A lightweight fork of etherpad based on javascript"
arch=(any)
url="https://github.com/ether/etherpad-lite"
license=('GPL')
groups=()
depends=('curl' 'python' 'gcc' 'openssl' 'nodejs')
makedepends=('git' 'gzip')
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
source=(etherpad-lite-bin etherpad-lite-daemon)
noextract=()
md5sums=('606113188c0baa6e94395660827f966a'
         '1e29912ff6015ce004b1d4e3d07f7ff1')

_gitroot='git://github.com/ether/etherpad-lite'
_gitname='master'

build() {
  cd "$srcdir"

  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  #
  # BUILD HERE
  #
  ./bin/installDeps.sh
}

package() {
  cd "$srcdir/$_gitname-build"
  mkdir -p $pkgdir/usr/share/etherpad-lite
  cp -r * $pkgdir/usr/share/etherpad-lite
  mkdir -p $pkgdir/usr/bin
  cp $srcdir/etherpad-lite-bin $pkgdir/usr/bin/etherpad-lite
  mkdir -p $pkgdir/srv/etherpad-lite
  rm -r $pkgdir/usr/share/etherpad-lite/var
  ln -s /srv/etherpad-lite $pkgdir/usr/share/etherpad-lite/var
  mkdir -p $pkgdir/etc/rc.d
  cp $srcdir/etherpad-lite-daemon $pkgdir/etc/rc.d/etherpad-lite
}
