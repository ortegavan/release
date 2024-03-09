# Teste da lib semantic-release

Esta é uma prova de conceito para testar a lib `semantic-release` que automatiza o versionamento semântico - [SemVer](https://semver.org) - da aplicação.

Para esta POC foi criada uma aplicação em Angular e adicionado o Angular Material.

## Instalação

Para instalar a lib e demais pacotes necessários, execute o comando:

```bash
npm install --save-dev semantic-release @semantic-release/git
```

## Configuração

Crie o arquivo `.releaserc.js` na raiz do projeto com o seguinte conteúdo e depois o adicione ao `.gitignore`:

```javascript
module.exports = {
    branches: ["main"],
    plugins: [
        "@semantic-release/commit-analyzer",
        "@semantic-release/release-notes-generator",
        "@semantic-release/github",
        [
            "@semantic-release/git",
            {
                assets: ["package.json", "package-lock.json"],
                message: "docs: packages atualizados para versão ${nextRelease.version}",
            },
        ],
    ],
    prepareCmd: "npm version ${nextRelease.version} -m 'docs: %s'",
    verifyConditions: ["@semantic-release/github"],
    publish: ["@semantic-release/github"],
    repositoryUrl: "https://github.com/ortegavan/release",
    githubToken: "TOKEN",
};
```

Altere as propriedades de acordo com o seu projeto. No exemplo, a aplicação está sendo publicada no GitHub.

## Execução

Para executar o `semantic-release` execute o comando:

```bash
npx semantic-release
```

Em ambiente de desenvolvimento, foi necessário fornecer o token do GitHub para que a lib possa publicar a release. Para isso, execute o comando:

```bash
GH_TOKEN=TOKEN npx semantic-release --no-ci
```
