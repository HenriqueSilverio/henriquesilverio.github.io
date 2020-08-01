---
layout:     post
title:      "npm: Forçar resolução para versão específica"
date:       2020-08-01 16:00:00
summary:    Dica útil principalmente para corrigir alertas de segurança
categories: npm
---

![Alerta falha de segurança](/images/github-security-alert.png)

As vezes você pode receber um alerta de potencial falha de segurança em seu projeto e um `npm audit fix` não conseguir resolver de forma automática. 

Isso acontece pois a falha encontrada é de alguma dependência de algum pacote que o seu projeto usa, e não diretamente no pacote em si. 

Por exemplo: foi encontrada uma falha no `lodash`. Seu projeto não depende diretamente do `lodash` mas depende do `eslint`, e o `eslint` sim depende do `lodash`. Então até que o `package.json` do `eslint` seja atualizado com a versão do `lodash` que tenha a correção dessa falha, você pode contornar o problema forçando a instalação de uma versão específica.

Para isso faremos dois ajustes no `package.json` do nosso projeto.

Primeiro adicione uma propriedade `resolutions`, e nela coloque o pacote e a versão que deseja forçar a instalar.

```json
{
  "resolutions": {
    "lodash": "^4.17.19"
  }
}
```

Depois na propriedade `scripts`, adicione um `preinstall` assim:


```json
"scripts": {
  "preinstall": "npx npm-force-resolutions"
}
```

Feito isso basta rodar um `npm i` para instalar as dependências e pronto!