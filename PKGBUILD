#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>


pkgname=stackedit
pkgver=5.14.10

pkgrel=3
pkgdesc='In-browser markdown editor'
arch=('any')
url='https://stackedit.io/'
license=('APACHE')
depends=('nodejs' 'chromium')
makedepends=('bower' 'gulp' 'npm')
options=(!strip)
source=("https://github.com/benweet/$pkgname/archive/v${pkgver}.tar.gz"
	$pkgname.sh
	$pkgname.desktop
	$pkgname.service)

install=$pkgname.install
pkgext='.pkg.tar'

build(){
  cd $pkgname-$pkgver
  npm install
  bower install
  npm install bower
  gulp
}

package() {
  cd $pkgname-$pkgver
  #Create folder for user $pkgname
  install -dm755 $pkgdir/var/lib/$pkgname
  cp -r * $pkgdir/var/lib/$pkgname/

  install -vDm755 $srcdir/$pkgname.sh $pkgdir/usr/bin/$pkgname
  install -vDm644 $srcdir/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop
  install -vDm644 chrome-app/logo-128.png $pkgdir/usr/share/pixmaps/$pkgname.png

  #Create systemd service
  install -Dm644 $srcdir/$pkgname.service $pkgdir/usr/lib/systemd/system/$pkgname.service
}

sha512sums=('f6e6b1c30f66c1bee3e0a2259f193edfc0c778e514ffeb8b9b71f6577f0f845a29c89c9abe5f856a6198e261dd8f2e49be5275e321f62194c568649a9f7ef2ee'
            '86df825566f2f8b704a51cf5e98212bc551d2a41a5466fb36874a573ecf3d47a5dcef70f424d0441de3244b2a3dd9b8bb1e922e1c98ba563ee32ae7b9a9a41c0'
            '12fe6adae83deb64cf3c40b3c9357e33007716fa2e38f2a9653004c53a25c8c8be03b8d19a14625f66d0cbbceea70a2b0b0d25747a6cc646be7629717d55964f'
            'c4572a6466ea107de5ffd3e2af7598e6fc5f4da09b6ddcc61eee817d01dd2ff2881e7fbcc3155fb391e5862066eefdc34d075f62bd4fced47290ac69e7757929')
