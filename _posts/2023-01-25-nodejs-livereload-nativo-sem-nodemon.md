---
layout:     post
title:      "Node.js: Livereload nativo (sem nodemon)"
date:       2023-01-25 20:22:00
summary:    Talvez você não precise instalar esse pacote.
categories: nodejs
---

Dica rápida: A partir do Node.js v18.11.0, temos um "watch mode" nativo! 

Como assim?

Sabe aquela coisa chata, de ter que ficar reiniciando sua aplicação toda hora enquanto está desenvolvendo, fazendo alterações? 

Talvez você até já use o nodemon (ou algum outro pacote de terceiros) para resolver essa questão...

Porém agora, não precisamos instalar mais nada para isso (pelo menos, não em boa parte dos casos).

Com o Node.js >= 18.11, basta iniciar sua aplicação com a flag [`--watch`](https://nodejs.org/dist/latest-v18.x/docs/api/cli.html#--watch), e qualquer alteração nos arquivos observados irá reiniciar o processo. Por padrão, o entrypoint e todos os arquivos importados nele serão observados.

Exemplo:

```bash
node --watch index.js
```

Show né? Simples assim! o/
