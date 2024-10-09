# Maintainer: pappy <pa314159@users.noreply.github.com>

_version=3.70.2
_patch=01

pkgname=nexus-oss
pkgver=${_version}.${_patch}
pkgrel=1
pkgdesc='Nexus 3 Repository OSS'
arch=('any')
url='http://nexus.sonatype.org'
license=("custom:$pkgname")
depends=('java-runtime-headless=11')
optdepends=('java-runtime-headless=17: you are advised to switch to Java 17 after migration')
provides=($pkgname)
backup=("var/lib/$pkgname/etc/nexus.properties"
		"usr/lib/$pkgname/bin/nexus.vmoptions"
		)
source=(
		"https://download.sonatype.com/nexus/3/nexus-$_version-$_patch-unix.tar.gz"
		"https://download.sonatype.com/nexus/nxrm3-migrator/nexus-db-migrator-$_version-$_patch.jar"
		"$pkgname.install"
		"$pkgname.properties"
		"$pkgname.service"
		"$pkgname.sysusers"
		"$pkgname.tmpfiles"
		"$pkgname.vmoptions"
		"pref_jre.cfg"
		)
sha256sums=('3f7bd2e7e42706af3ffa288a1e9728a3bb33e04470a9c2625e7444299e0a7e87'
            '69aebd05589a730af54d7b2cacba7d7bb5ea1f13dccd5e0d7eec002837068df0'
            '04a299ed31faa4bdc2dc2cf59d52b04d4c161807c0182c23f8b890f030d2992a'
            '9353c02a2a69a11a79e9149b6465a810e4b083b5ef168779cfe8385f1a27ae60'
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

	install -Dm644 nexus-db-migrator-$_version-$_patch.jar $pkgdir/usr/lib/$pkgname/bin/nexus-db-migrator.jar

	install -Dm640 $srcdir/$pkgname.properties $pkgdir/var/lib/$pkgname/etc/nexus.properties
	install -Dm644 $srcdir/$pkgname.vmoptions $pkgdir/usr/lib/$pkgname/bin/nexus.vmoptions
	install -Dm644 $pkgname.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
	install -Dm644 $pkgname.tmpfiles "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
	install -Dm644 $pkgname.sysusers "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
	install -m644 pref_jre.cfg $pkgdir/usr/lib/$pkgname/.install4j
	install -Dm644 $srcdir/nexus-$_version-$_patch/OSS-LICENSE.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE

	pushd $pkgdir/usr/lib/$pkgname
	rm -rf bin/nexus.rc bin/contrib *LICENSE.txt
	popd

	chmod -R o-rwx $pkgdir/var/lib/$pkgname
}

