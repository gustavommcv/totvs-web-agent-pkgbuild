pkgname=totvs-web-agent
pkgver=1.0.0
pkgrel=1
pkgdesc="TOTVS Web Agent para integração com Protheus."
arch=('x86_64')
license=('custom')
depends=(
    'glibc'
    'libappindicator-gtk3'
    'libindicator-gtk3'
)
source=(
    "web-agent-linux-x64.deb"
    "web-agent.ini"
)
sha256sums=('SKIP' 'SKIP')

package() {
    cd "$srcdir"

    #
    # 1 — Extrair o .deb
    #
    bsdtar -xf "$srcdir/web-agent-linux-x64.deb"

    #
    # 2 — Extrair o data.tar.gz
    #
    bsdtar -xf data.tar.gz

    #
    # 3 — Copiar /opt/web-agent
    #
    install -d "$pkgdir/opt/web-agent"
    cp -r "$srcdir/opt/web-agent/"* "$pkgdir/opt/web-agent/"

    #
    # 4 — Substituir o arquivo de configuração web-agent.ini
    #
    install -Dm644 "$srcdir/web-agent.ini" \
        "$pkgdir/opt/web-agent/web-agent.ini"

    #
    # 5 — Copiar atalhos .desktop
    #
    install -d "$pkgdir/usr/share/applications"
    cp "$srcdir/usr/share/applications/web-agent.desktop" \
       "$pkgdir/usr/share/applications/totvs-web-agent.desktop"

    #
    # 6 — Copiar ícones
    #
    install -d "$pkgdir/usr/share/icons"
    cp -r "$srcdir/usr/share/icons/"* "$pkgdir/usr/share/icons/"

    #
    # 7 — Changelog
    #
    install -d "$pkgdir/usr/share/doc/web-agent"
    cp "$srcdir/usr/share/doc/web-agent/changelog.gz" \
       "$pkgdir/usr/share/doc/web-agent/"

    #
    # 8 — Criar /usr/bin/totvs-web-agent (wrapper)
    #
    install -d "$pkgdir/usr/bin"
    cat << EOF > "$pkgdir/usr/bin/totvs-web-agent"
#!/bin/bash
exec /opt/web-agent/web-agent "\$@"
EOF

    chmod +x "$pkgdir/usr/bin/totvs-web-agent"
}
