# Maintainer: pappy <pa314159@users.noreply.github.com>

_version=3.70.0
_patch=03

pkgname=nexus-oss
pkgver=${_version}.${_patch}
pkgrel=1
pkgdesc='Nexus 3 Repository OSS'
arch=('any')
url='http://nexus.sonatype.org'
license=("custom:$pkgname")
depends=('java-runtime-headless=11')
replaces=('nexus3')
provides=($pkgname)
backup=("var/lib/$pkgname/etc/nexus.properties"
		"usr/lib/$pkgname/bin/nexus.vmoptions"
		)
source=(
		"https://download.sonatype.com/nexus/3/nexus-$_version-$_patch-unix.tar.gz"
		"$pkgname.install"
		"$pkgname.properties"
		"$pkgname.service"
		"$pkgname.sysusers"
		"$pkgname.tmpfiles"
		"$pkgname.vmoptions"
		"pref_jre.cfg"
		)
sha256sums=('892dd992343cef3fb7f1d48ad18c9bd55837cc712f651ba7d991aeb7d2d6ce86'
            '938c04841139a231891e367220af57fe10c93b8d7b9bd49c8732fbf461a120f8'
            'dcdef5614db12f38b3da0b9de1b52fb7fa402af6621a825981c6168a34a6ad9b'
            '28d947b261c9087a16b0d5313aae92deccb03d4e109102eb702f4ab7e4899f44'
            '77d699b5ccf6387fa2f69df2cd71cdb75b4ffbf46a10110dd6c0e2802783dbef'
            'efd66ac28e622cdf58f5733bdced6654b170558834c3e4304b3a2dfb7d964994'
            '91ecb4f23b8a68ce7f1c7a9307dcbc745244a51173feec0fc47c5587b7769ab3'
            'd713e29b72522fe4395b6959d27e2a98a24961393e08df7a6b022b1fd77c650d')

install=$pkgname.install

package() {
	install -dm755 $pkgdir/usr/lib
	install -dm750 $pkgdir/var/lib/$pkgname
	install -dm750 $pkgdir/var/log/$pkgname

	cp -a $srcdir/nexus-$_version-$_patch $pkgdir/usr/lib/$pkgname

	pushd $pkgdir/usr/lib/$pkgname
	rm -rf bin/nexus.rc \
		bin/contrib \
		LICENSE.txt
	popd

	install -Dm640 $srcdir/$pkgname.properties $pkgdir/var/lib/$pkgname/etc/nexus.properties

	install -Dm644 $srcdir/nexus-$_version-$_patch/OSS-LICENSE.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE
	install -Dm644 $srcdir/$pkgname.vmoptions $pkgdir/usr/lib/$pkgname/bin/nexus.vmoptions
	install -Dm644 $pkgname.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
	install -Dm644 $pkgname.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
	install -Dm644 $pkgname.sysusers "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
	install -m644 pref_jre.cfg $pkgdir/usr/lib/$pkgname/.install4j

	chmod -R o-rwx $pkgdir/var/lib/$pkgname
}

