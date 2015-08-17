# Maintainer: Troy Cox <troy.cox@rackspace.com>

pkgname=python-supernova-git
pkgver=20120725
pkgrel=1
pkgdesc="Use novaclient with multiple OpenStack nova environments the easy way"
arch=('i686' 'x86_64')
url="http://github.com/rackerhacker/supernova"
license=('GPL')
depends=('python2' 'python-keyring')
#optdepends=('')
makedepends=('python2' 'git')
conflicts=('python-supernova')
_gitroot='https://github.com/rackerhacker/supernova.git'
_gitname='supernova'

build() {
        cd "${srcdir}"
        msg "Connecting to GIT server...."

        if [[ -d "${_gitname}" ]]; then
        cd "${_gitname}" && git pull origin
        msg "The local files are updated."
        else
        git clone "${_gitroot}" "${_gitname}"
        fi

        msg "GIT checkout done or server timeout"
        msg "Starting make..."

        rm -rf "$srcdir/$_gitname-build"
        git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
        REV=$(git show-ref --abbrev --heads | cut -f 1 -d\ )
        cd "$srcdir/$_gitname-build"
        python2 setup.py build || return 1
        python2 setup.py install --root=${pkgdir} || return 1
}

