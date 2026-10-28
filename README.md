# VP Painel (APK)

Aplicativo Android do painel do **Viver Presente** para a equipe de gestão. O app é um invólucro (Trusted Web
Activity) do painel publicado em `https://viverpresenteyoga.com.br/painel.html`, que leva cada conta ao seu painel
(administração ou master): quadro do projeto, curadoria, correio da equipe, cadastros recebidos, indicadores e avisos no celular.

## Como obter o APK

Cada envio para a branch `main` gera um APK automaticamente (GitHub Actions) e o publica na página
**Releases** deste repositório. No celular, abra a release mais recente, baixe o arquivo `.apk` e instale.
Se o aparelho perguntar, permita a instalação a partir do navegador.

Para gerar de novo sem mudar nada: aba **Actions** → *Gerar APK* → *Run workflow*.

## Assinatura

Sem segredos configurados, o APK sai com uma chave **provisória**, criada a cada compilação: serve para testar,
mas uma versão nova não instala por cima da anterior sem desinstalar antes.

Para a assinatura **oficial** (atualizações instalam por cima e o app abre em tela cheia, sem a barra do navegador),
cadastre em *Settings → Secrets and variables → Actions*:

| Segredo | Conteúdo |
|---|---|
| `KEYSTORE_B64` | o arquivo `.keystore` em base64 |
| `KEYSTORE_PASSWORD` | senha do keystore |
| `KEY_PASSWORD` | senha da chave (alias `vpapk`) |

O site publica a impressão digital da chave oficial em `/.well-known/assetlinks.json`; é isso que permite ao
Android abrir o app em tela cheia.

## Estrutura

- `app/` projeto Android (sem código próprio: usa `androidbrowserhelper`)
- `app/src/main/AndroidManifest.xml` endereço inicial, cores e ícones
- `.github/workflows/apk.yml` compilação e publicação

Requisitos para compilar localmente: JDK 17, Android SDK 34 e Gradle 8.7 (`gradle assembleRelease`).
