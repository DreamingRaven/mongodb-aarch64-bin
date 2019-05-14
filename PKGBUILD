# Maintainer: George Raven <GeorgeRavenCommunity AT pm Dot me>
# adapted from: Ali Molaei https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=mongodb-bin

pkgname="mongodb-arm-bin"
basever="4.0"
pkgver="${basever}.9"
pkgrel="1"
pkgdesc="A high-performance, open source, schema-free document-oriented database"
arch=("aarch64")
url="https://www.mongodb.com/"
license=("SSPLv1")
provides=("mongodb=$pkgver")
conflicts=("mongodb")
optdepends=("mongodb-tools: The MongoDB tools provide import, export, and diagnostic capabilities.")
source=(
    "https://repo.mongodb.org/apt/ubuntu/dists/xenial/mongodb-org/${basever}/multiverse/binary-arm64/mongodb-org-shell_${pkgver}_arm64.deb"
    "https://repo.mongodb.org/apt/ubuntu/dists/xenial/mongodb-org/${basever}/multiverse/binary-arm64/mongodb-org-server_${pkgver}_arm64.deb"
    "https://repo.mongodb.org/apt/ubuntu/dists/xenial/mongodb-org/${basever}/multiverse/binary-arm64/mongodb-org-mongos_${pkgver}_arm64.deb"
    "mongodb.service"
    "mongodb.conf"
    "mongodb.sysusers"
    "mongodb.tmpfiles"
    "LICENSE")
sha256sums=("SKIP")

backup=("etc/mongodb.conf")

prepare() {
  cd "${srcdir}"
  mkdir -p "${srcdir}/output"

  # pkgbuild automatically unpacked the first one for us
  # ar x mongodb-org-mongos_${pkgver}_arm64.deb
  tar -xvf "${srcdir}/data.tar.xz" -C "${srcdir}/output" #mongos extracted
  ar x mongodb-org-server_${pkgver}_arm64.deb
  tar -xvf "${srcdir}/data.tar.xz" -C "${srcdir}/output" #server extracted
  ar x mongodb-org-shell_${pkgver}_arm64.deb
  tar -xvf "${srcdir}/data.tar.xz" -C "${srcdir}/output" #shell extracted
}

package() {
  mkdir -p "$pkgdir/usr"
  mkdir -p "$pkgdir/usr/share/man"
  cp -r "$srcdir/output/usr/bin" "$pkgdir/usr/"
  cp -r "$srcdir/output/usr/share/man/man1" "$pkgdir/usr/share/man/"
  install -Dm644 "$srcdir/mongodb.conf" "$pkgdir/etc/mongodb.conf"
  install -Dm644 "$srcdir/mongodb.service" "$pkgdir/usr/lib/systemd/system/mongodb.service"
  install -Dm644 "$srcdir/mongodb.sysusers" "$pkgdir/usr/lib/sysusers.d/mongodb.conf"
  install -Dm644 "$srcdir/mongodb.tmpfiles" "$pkgdir/usr/lib/tmpfiles.d/mongodb.conf"
  install -Dm644 "$srcdir/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
