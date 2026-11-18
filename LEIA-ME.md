# Estante — app Android

App de leitura e busca de citações, organizado como uma estante: Escritos de Santa Ângela Merici (Recomendações e Testamento, tradução das Religiosas Ursulinas da União Romana) e a encíclica Laudato Si’ do Papa Francisco. Funciona 100% offline: os textos e as fontes estão dentro do app.

## O que tem aqui

| Pasta / arquivo | O que é |
|---|---|
| `www/index.html` | O app inteiro (texto, fontes, telas). É o único arquivo que você edita para mudar conteúdo ou visual. |
| `android/` | Projeto Android nativo (Capacitor 8), pronto para compilar. |
| `assets/` | Ícone e tela de abertura em alta resolução. |
| `escritos-santa-angela.md` e `laudato-si.md` | Os textos digitalizados e revisados, em formato simples. |
| `.github/workflows/build-apk.yml` | Gera o APK automaticamente no GitHub. |

## Jeito mais fácil de gerar o APK: GitHub (sem instalar nada)

1. Crie um repositório no GitHub e envie esta pasta inteira (sem `node_modules`).
2. Abra a aba **Actions** do repositório. A compilação “Gerar APK” começa sozinha a cada envio (ou clique em *Run workflow*).
3. Quando terminar (uns 5 minutos), abra a execução e baixe o arquivo **escritos-santa-angela-apk**.
4. Descompacte, passe o `app-debug.apk` para o celular e instale (o Android vai pedir para permitir “instalar apps desconhecidos”).

## Pelo Android Studio

Requisitos: Node.js 22+, Android Studio (com JDK 21).

```bash
npm install
npx cap sync android
npx cap open android
```

No Android Studio: **Build › Build App Bundle(s) / APK(s) › Build APK(s)**. Para testar direto no celular, conecte-o via USB e clique em **Run**.

## Publicar na Google Play

A Play Store pede um **AAB assinado**. No Android Studio: **Build › Generate Signed App Bundle / APK**, crie uma chave (guarde o arquivo `.jks` e as senhas em local seguro: sem eles não é possível publicar atualizações) e envie o `.aab` pelo Google Play Console.

Antes de publicar, troque o identificador do app `br.com.escritossantaangela.app` em `capacitor.config.json` e em `android/app/build.gradle` (`applicationId`) por um domínio da instituição, se desejar.

## Alterar o conteúdo

Edite `www/index.html` e rode `npx cap sync android` antes de compilar de novo. Os textos estão no início do bloco `<script>` (constantes `ESC` e `LS`), organizados por livro, seção e parágrafo.
