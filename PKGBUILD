# Maintainer: Jesus Alvarez <jeezusjr at gmail dot com>
#
# This PKGBUILD was generated by the archzfs build scripts located at
#
# http://github.com/archzfs/archzfs
#
# ! WARNING !
#
# The archzfs packages are kernel modules, so these PKGBUILDS will only work with the kernel package they target. In this
# case, the archzfs-linux-zen packages will only work with the default linux-zen package! To have a single PKGBUILD target many
# kernels would make for a cluttered PKGBUILD!
#
# If you have a custom kernel, you will need to change things in the PKGBUILDS. If you would like to have AUR or archzfs repo
# packages for your favorite kernel package built using the archzfs build tools, submit a request in the Issue tracker on the
# archzfs github page.
#
pkgbase="zfs-linux-zen-git"
pkgname=("zfs-linux-zen-git" "zfs-linux-zen-git-headers")

pkgver=2018.06.11.r4594.gc634808eb.4.16.13.2
pkgrel=1
makedepends=("linux-zen-headers=4.16.13-2" "git")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("git+https://github.com/zfsonlinux/zfs.git#commit=c634808ebbc86fc0eac498bcb17adda407da5569")
sha256sums=("SKIP")
license=("CDDL")
depends=("kmod" "zfs-utils-common-git=2018.06.11.r4594.gc634808eb" "linux-zen=4.16.13-2")

build() {
    cd "${srcdir}/zfs"
    ./autogen.sh
    ./configure --prefix=/usr --sysconfdir=/etc --sbindir=/usr/bin --libdir=/usr/lib \
                --datadir=/usr/share --includedir=/usr/include --with-udevdir=/lib/udev \
                --libexecdir=/usr/lib/zfs-0.7.9 --with-config=kernel \
                --with-linux=/usr/lib/modules/4.16.13-2-zen/build \
                --with-linux-obj=/usr/lib/modules/4.16.13-2-zen/build
    make
}

package_zfs-linux-zen-git() {
    pkgdesc="Kernel modules for the Zettabyte File System."
    install=zfs.install
    provides=("zfs")
    groups=("archzfs-linux-zen-git")
    conflicts=('zfs-linux-zen' 'spl-linux-zen-git')
    replaces=("spl-linux-zen-git")
    cd "${srcdir}/zfs"
    make DESTDIR="${pkgdir}" install
    cp -r "${pkgdir}"/{lib,usr}
    rm -r "${pkgdir}"/lib
    # Remove src dir
    rm -r "${pkgdir}"/usr/src
}

package_zfs-linux-zen-git-headers() {
    pkgdesc="Kernel headers for the Zettabyte File System."
    conflicts=('zfs-archiso-linux-headers' 'zfs-archiso-linux-git-headers' 'zfs-linux-hardened-headers' 'zfs-linux-hardened-git-headers' 'zfs-linux-lts-headers' 'zfs-linux-lts-git-headers' 'zfs-linux-headers' 'zfs-linux-git-headers' 'zfs-linux-vfio-headers' 'zfs-linux-vfio-git-headers' 'zfs-linux-zen-headers'  )
    cd "${srcdir}/zfs"
    make DESTDIR="${pkgdir}" install
    rm -r "${pkgdir}/lib"
    # Remove reference to ${srcdir}
    sed -i "s+${srcdir}++" ${pkgdir}/usr/src/zfs-*/4.16.13-2-zen/Module.symvers
}
