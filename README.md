# TOTVS Web Agent — PKGBUILD para Arch Linux

Este repositório contém um **PKGBUILD totalmente funcional** para instalar o **TOTVS Web Agent** no Arch Linux e derivados (Manjaro, Omarchy, EndeavourOS, CachyOS, etc.) usando o `makepkg` ou qualquer AUR helper.

O Web Agent é utilizado por aplicações TOTVS para comunicação segura entre o navegador e o ambiente local por meio de WebSocket (`wss://127.0.0.1:21021/agent`).

---

## Funcionalidades

- Instala o Web Agent em `/opt/web-agent`
- Copia automaticamente certificados e chave privada
- Instala `.desktop`, ícones e documentação
- Gera pacote `totvs-web-agent` e `totvs-web-agent-debug`
- Inclui e instala `web-agent.ini`
- 100% compatível com o ecossistema Arch

---

## Estrutura instalada

```
/opt/web-agent/
├── web-agent
├── web-agent.png
├── web-agent.ini
├── cacert.pem
├── totvs_certificate.crt
├── totvs_certificate_CA.crt
├── totvs_certificate_key.pem
├── printer
└── pdfprinter

/usr/share/applications/web-agent.desktop
/usr/share/icons/hicolor/*/apps/web-agent.png
/usr/share/doc/web-agent/changelog.gz
```

---

## Como instalar

### 1. Clone o repositório

```bash
git clone https://github.com/gustavommcv/totvs-web-agent-pkgbuild.git
cd totvs-web-agent-pkgbuild
```

### 2. Coloque o arquivo .deb do web agent no diretório

O arquivo deve se chamar:

```
web-agent-linux-x64.deb
```

### 3. Compile e instale

```bash
makepkg -fsi
```

---

# Ativando o Certificado do Web Agent no Navegador

O Web Agent utiliza um **certificado self-signed embutido no binário**.  
O navegador **não confia automaticamente**, então você **PRECISA autorizar o certificado** para que o Protheus WebApp funcione sem erro.

Sem aceitar o certificado, você verá erros como:

```
net::ERR_CERT_AUTHORITY_INVALID
Firefox can’t establish a connection to the server at wss://127.0.0.1:21021/agent
```


### ✅ Como ativar o certificado

Abra no seu navegador:
```
https://127.0.0.1:21021
```

O navegador exibirá uma tela de segurança.

Clique em:

- **Firefox:**  
  ➤ *Avançado* → *Aceitar o risco e continuar*

- **Chrome / Brave / Edge:**  
  ➤ *Avançado* → *Ir para 127.0.0.1 (não seguro)*

Após aceitar, o navegador criará uma exceção permanente de confiança.

### 📌 Você só precisa fazer isso UMA vez.

--- 

## Comandos úteis

Verificar se está rodando

```bash
ps aux | grep web-agent
```

Ver porta ativa

```bash
sudo lsof -i -P -n | grep 21021
```

Testar TLS

```bash
openssl s_client -connect 127.0.0.1:21021
```

Abre o Web Agent pelo terminal

```bash
totvs-web-agent
```

---

## Licença

Este repositório contém apenas o PKGBUILD.
Os binários e certificados do Web Agent pertencem à TOTVS.

---

## Contribuições

Contribuições são bem-vindas!
Issues e PRs podem ser abertos livremente.
