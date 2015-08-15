# Maintainer : adytzu2007 <adybac at gmail {dot} com>
# Contributor: Samsagax <samsagax at gmail {dot} com>

pkgname=dkms-bbswitch-git
pkgver=20130317
pkgrel=1
pkgdesc="kernel module allowing to switch dedicated graphics card on Optimus laptops, dkms version"
arch=('i686' 'x86_64')
url=("http://github.com/Bumblebee-Project/bbswitch")
license=('GPL')
provides=('bbswitch')
conflicts=('bbswitch-git' 'bbswitch' 'dkms-bbswitch')
depends=('dkms' 'linux-headers')
makedepends=('git')
install=dkms-bbswitch.install

_gitroot='git://github.com/Bumblebee-Project/bbswitch.git'
_gitname='bbswitch'
_gitbranch='develop'

build()
{
    cd ${srcdir}

    # git checkout
    if [ -d ${srcdir}/${_gitname} ] ; then
        msg "Git checkout:  Updating existing tree"
        cd ${_gitname} && git pull origin
        msg "Git checkout:  Tree has been updated"
    else
        msg "Git checkout:  Retrieving sources"
        git clone --depth=1 ${_gitroot} ${_gitname} --branch ${_gitbranch}
    fi

    msg "Checkout completed"

    cd ${srcdir}/${_gitname}
cat > dkms.conf <<EOF
PACKAGE_NAME="bbswitch"
PACKAGE_VERSION="${pkgver}"
MAKE[0]="make"
CLEAN="clean"
BUILT_MODULE_NAME[0]="bbswitch"
DEST_MODULE_LOCATION[0]="/kernel/drivers/acpi"
AUTOINSTALL="yes"
EOF
}

package()
{
  cd ${srcdir}/${_gitname}
  install -dm755 "${pkgdir}/usr/src/bbswitch-${pkgver}/"
  cp -r * ${pkgdir}/usr/src/bbswitch-${pkgver}/
}
