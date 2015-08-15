# Maintainer: Claudio Kozicky <claudiokozicky@gmail.com>
# Contributor: Zachary A. Jones <JazzplayerL9@gmail.com>

pkgname=bittripbeat
_pkgname=bit.trip.beat
pkgver=1.0_5
_pkgver=1346093242
pkgrel=3
pkgdesc="Rhythm-based pong-style platformer."
arch=(i686 x86_64)
url="http://bittripgame.com/bittrip-beat.html"
license=(custom)
depends=(libgl libvorbis openal sdl)
source=($pkgname.sh)
md5sums=(b20f57564d15776df416ee1ee3efcbfd)
[ $CARCH = i686 ] \
    && source+=(hib://"$_pkgname"_${pkgver//_/-}_i386-$_pkgver.tar.gz) \
    && md5sums+=(3ff9af36f309d6b7ce00b0193c2fdbd7)
[ $CARCH = x86_64 ] \
    && source+=(hib://"$_pkgname"_${pkgver//_/-}_amd64-$_pkgver.tar.gz) \
    && md5sums+=(0e5cb808224b0912736871e6d4504091)
DLAGENTS+=('hib::/usr/bin/echo Could not find %u. Manually download it to \"$(pwd)\", or set up a hib:// DLAGENT in /etc/makepkg.conf.; exit 1')
PKGEXT=.pkg.tar

prepare()
{
    # fix .desktop file
    sed -e "/Path=.*/ D" \
        -e "/Exec=.*/ s/\.//g" \
        -e "s;Icon=.*;Icon=/usr/share/pixmaps/$pkgname.png;" \
        -i "$srcdir"/$_pkgname-${pkgver/%_*}/$_pkgname.desktop
}
    
package()
{
    # data
    cd "$srcdir"/$_pkgname-${pkgver/%_*}
    find $_pkgname -name BEAT.png -prune -o -type f -exec install -Dm644 {} "$pkgdir"/opt/{} \;
    chmod +x "$pkgdir"/opt/$_pkgname/$_pkgname

    # doc
    install -d "$pkgdir"/usr/share/doc/$pkgname 
    install -m644 -t "$pkgdir"/usr/share/doc/$pkgname README README.html

    # desktop integration
    install -Dm644 $_pkgname/BEAT.png "$pkgdir"/usr/share/pixmaps/$pkgname.png
    install -Dm644 $_pkgname.desktop "$pkgdir"/usr/share/applications/$pkgname.desktop

    # launcher
    cd ..
    install -Dm755 $pkgname.sh "$pkgdir"/usr/bin/$pkgname
}

# vim:et:sw=4:sts=4
