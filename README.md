# Teste da lib semantic-release

Esta é uma prova de conceito para testar a lib `semantic-release` que automatiza o versionamento semântico - [SemVer](https://semver.org) - da aplicação.

Para esta POC foi criada uma aplicação em Angular e adicionado o Angular Material.

## Instalação

Para instalar a lib e demais pacotes necessários, execute o comando:

```bash
npm install --save-dev semantic-release @semantic-release/changelog @semantic-release/git @semantic-release/npm
```

## Configuração

Crie o arquivo `.releaserc.js` na raiz do projeto com o seguinte conteúdo e depois o adicione ao `.gitignore`:

```javascript
module.exports = {
    branches: ["main"],
    plugins: ["@semantic-release/commit-analyzer", "@semantic-release/release-notes-generator", ["@semantic-release/npm", { npmPublish: false }], "@semantic-release/github"],
    verifyConditions: ["@semantic-release/npm", "@semantic-release/github"],
    publish: ["@semantic-release/github"],
    repositoryUrl: "https://github.com/ortegavan/release.git",
    githubToken: "[SEU TOKEN]",
};
```

Altere as propriedades de acordo com o seu projeto. No exemplo, a aplicação está sendo publicada no GitHub pulando a etapa de publicação de pacotes no npm.

## Execução

Para executar o `semantic-release` execute o comando:

```bash
npx semantic-release --no-ci
```

Em ambiente de desenvolvimento, foi necessário fornecer o token do GitHub para que a lib possa publicar a release. Para isso, execute o comando:

```bash
GH_TOKEN=[SEU TOKEN] npx semantic-release --no-ci
```
