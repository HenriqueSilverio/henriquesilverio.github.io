---
layout:     post
title:      "Node.js: Variáveis de ambiente nativas (sem dependências)"
date:       2025-02-15 20:11:00
summary:    Mais uma da série "Talvez você não precise instalar esse pacote".
categories: nodejs
---

A partir da versão >= 20.6, já é possível trabalhar com **variáveis de ambiente no Node.js** de forma nativa, sem precisar instalar pacotes de terceiros.

Para isso, basta usar a opção <a target="_blank" href="https://nodejs.org/dist/latest-v22.x/docs/api/cli.html#--env-fileconfig">--env-file</a>.

Assumindo que você já tenha criado um arquivo `.env` na raíz do seu projeto, basta rodar o seguinte comando:

```bash
node --env-file=.env index.js
```

Pronto! Sua aplicação irá iniciar já com todas as variáveis de ambiente do arquivo `.env` carregadas, que como de costume, estarão disponíveis no `process.env`.

## Variáveis em múltiplos arquivos

Se desejar, você também pode separar suas variáveis de ambiente em arquivos diferentes.

Por exemplo, nesse caso, as variáveis do `.dev.env` irão sobrescrever as variáveis do `.env`.

```bash
node --env-file=.env --env-file=.dev.env index.js
```

## Arquivo de configuração opcional

Por padrão, a `--env-file` irá disparar um erro caso o arquivo informado não exista.

Caso você não queira que isso aconteça, é possível usar uma outra opção: <a target="_blank" href="https://nodejs.org/dist/latest-v22.x/docs/api/cli.html#--env-file-if-existsconfig">--env-file-if-exists</a>, introduzida no Node.js v22.9.

```bash
node --env-file-if-exists=.env index.js
```

O comportamento dessa opção é o mesmo da `--env-file`, porém, não irá disparar um erro caso o arquivo informado não exista.
