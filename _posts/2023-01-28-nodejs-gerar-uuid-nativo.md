---
layout:     post
title:      "Node.js: UUID nativo (sem depedências)"
date:       2023-01-28 14:08:00
summary:    Talvez você não precise instalar esse pacote.
categories: nodejs
---

O Universally Unique Identifier / Identificador Único Universal, mais conhecido como UUID (também conhecido por alguns como Globally Unique Identifier, ou GUID), é um dos formatos mais confiáveis (até o momento), para identificar informações de forma única, com um risco de colisão quase nulo.

Em diversos tutoriais sobre Node.js, é muito comum vermos o uso de uma biblioteca externa (ex: <a target="_blank" href="https://github.com/uuidjs/uuid">uuid</a>) para gerar UUID's.

Porém, o que muitos ainda não sabem, é que, se você usa qualquer versão do Node.js >= 14.17, na maioria dos casos, essa biblioteca não é mais necessária!

**Dica rápida:** A partir do <a target="_blank" href="https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V14.md#uuid-support-in-the-crypto-module">Node.js v14.17.0</a>, temos um <a target="_blank" href="https://github.com/nodejs/node/blob/main/doc/changelogs/CHANGELOG_V14.md#uuid-support-in-the-crypto-module">método nativo para gerar UUID's v4</a>!

Exemplo:

```javascript
import { randomUUID } from 'crypto'

randomUUID()

// Returna um UUID v4 aleatório, ex:
// '9e424b39-6fd3-4606-b664-02da7445f5ba'
```

Show né? Simples assim! o/
