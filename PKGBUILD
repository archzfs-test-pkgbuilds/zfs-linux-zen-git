# Maintainer: Jan Houben <jan@nexttrex.de>
# Contributor: Jesus Alvarez <jeezusjr at gmail dot com>
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
_commit='73a5ec30bf6facf44a59045ea761a704c5e1b431'
_zfsver="2018.09.06.r4719.g73a5ec30b"
_kernelver="4.18.5.zen1-1"
_extramodules="${_kernelver/.zen/-zen}-zen"

pkgver="${_zfsver}_$(echo ${_kernelver} | sed s/-/./g)"
pkgrel=1
makedepends=("linux-zen-headers=${_kernelver}" "git")
arch=("x86_64")
url="http://zfsonlinux.org/"
source=("git+https://github.com/zfsonlinux/zfs.git#commit=${_commit}"
        "upstream-ac09630-Fix-zpl_mount-deadlock.patch"
        "upstream-9f64c1e-Linux-4.18-compat-inode-timespec_timespec64.patch"
        "upstream-9161ace-Linux-compat-4.18-check_disk_size_change.patch")
sha256sums=("SKIP" 
            "1799f6f7b2a60a23b66106c9470414628398f6bfc10da3d0f41c548bba6130e8"
            "03ed45af40850c3a51a6fd14f36c1adc06501c688a67afb13db4fded6ec9db1d"
            "afbde4a2507dff989404665dbbdfe18eecf5aba716a6513902affa0e4cb033fe")
license=("CDDL")
depends=("kmod" "zfs-utils-common-git=${_zfsver}" "linux-zen=${_kernelver}")

build() {
    cd "${srcdir}/zfs"
    ./autogen.sh
    ./configure --prefix=/usr --sysconfdir=/etc --sbindir=/usr/bin --libdir=/usr/lib \
                --datadir=/usr/share --includedir=/usr/include --with-udevdir=/lib/udev \
                --libexecdir=/usr/lib/zfs-${zfsver} --with-config=kernel \
                --with-linux=/usr/lib/modules/${_extramodules}/build \
                --with-linux-obj=/usr/lib/modules/${_extramodules}/build
    make
}

package_zfs-linux-zen-git() {
    pkgdesc="Kernel modules for the Zettabyte File System."
    install=zfs.install
    provides=("zfs")
    groups=("archzfs-linux-zen-git")
    conflicts=('zfs-linux-zen' 'spl-linux-zen-git' 'spl-linux-zen')
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
    sed -i "s+${srcdir}++" ${pkgdir}/usr/src/zfs-*/${_extramodules}/Module.symvers
}
