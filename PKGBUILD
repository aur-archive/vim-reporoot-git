# Maintainer: Andy Weidenbaum <archbaum@gmail.com>

pkgname=vim-reporoot-git
pkgver=20140704
pkgrel=1
pkgdesc="Change the directory to the root of the source code repository"
arch=('any')
depends=('vim')
makedepends=('git')
groups=('vim-plugins')
url="https://github.com/jmcantrell/vim-reporoot"
license=('custom:vim')
source=(${pkgname%-git}::git+https://github.com/jmcantrell/vim-reporoot)
sha256sums=('SKIP')
provides=('vim-reporoot')
conflicts=('vim-reporoot')
install=vimdoc.install

pkgver() {
  cd ${pkgname%-git}
  git log -1 --format="%cd" --date=short | sed "s|-||g"
}

package() {
  cd ${pkgname%-git}

  msg 'Installing appdirs...'
  install -dm 755 "$pkgdir/usr/share/vim/vimfiles"
  for _appdir in doc plugin; do
    cp -dpr --no-preserve=ownership $_appdir "$pkgdir/usr/share/vim/vimfiles/$_appdir"
  done

  msg 'Cleaning up pkgdir...'
  find "$pkgdir" -type d -name .git -exec rm -r '{}' +
  find "$pkgdir" -type f -name .gitignore -exec rm -r '{}' +
}
