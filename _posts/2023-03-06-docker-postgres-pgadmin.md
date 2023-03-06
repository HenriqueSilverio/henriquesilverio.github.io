---
layout:     post
title:      "PostgreSQL e pgAdmin para ambiente de desenvolvimento"
date:       2023-03-06 09:50:00
summary:    Setup fácil e rápido (com Docker Compose), para subir um banco de dados PostgreSQL e interface gráfica pgAdmin.
categories: database
---

Seja para estudos / experimentos, ou até para desenvolver aplicações completas, com o Docker fica bem mais simples de prover a infraestrutura que precisamos. Neste post, mostro como faço para subir o <a target="_blank" href="https://postgresql.org">PostgreSQL</a> e o <a target="_blank" href="https://pgadmin.org">pgAdmin</a> para ambiente de desenvolvimento.

Antes de tudo, você precisa ter o <a target="_blank" href="https://docker.com">Docker</a> (com Docker Compose) rodando em sua máquina.

Para rodar o Docker no Windows, você <del>deveria</del> pode utilizar o <a target="_blank" href="https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers">WSL</a>. Caso não saiba do que isso se trata, consulte a <a target="_blank" href="https://learn.microsoft.com/en-us/windows/wsl/">documentação da Microsoft</a>, ela está muito bem feita!

Na pasta raíz do seu projeto, crie um arquivo chamado `docker-compose.yaml`, com o seguinte conteúdo:

```yaml
version: "3.8"
services:
  postgres:
    image: postgres:15.2-alpine
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    ports:
      - 5432:5432
  pgadmin:
    depends_on:
      - postgres
    image: dpage/pgadmin4:6.20
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@host.com
      PGADMIN_DEFAULT_PASSWORD: secret
    ports:
      - 5480:80
```

Para iniciar os serviços, basta rodar o comando:

```bash
docker-compose up
```

Se preferir, você pode iniciar os serviços em background. Para isso, use a flag `-d`, assim:

```bash
docker-compose up -d
```

## Gerenciar o PostgreSQL com psql

Para testar o setup, podemos nos conectar ao Postgres usando o <a target="_blank" href="https://www.postgresql.org/docs/current/app-psql.html">psql</a> dentro do nosso container.

Execute o shell com o comando:

```bash
docker-compose exec postgres /bin/sh
```

Faça login no psql:

```bash
psql -U admin
```

Liste os bancos de dados:

```bash
\l
```

## Gerenciar o PostgreSQL com pgAdmin

Como alternativa ao psql, podemos utilizar uma interface gráfica para gerenciar o Postgres. Uma das opções aqui é o pgAdmin.

Em seu navegador preferido, acesse `http://localhost:5480`.

Faça login no pgAdmin com as credenciais: `admin@host.com` / `secret`.

## String de conexão PostgreSQL

Para conectar suas aplicações ao Postgres, basta informar a <a target="_blank" href="https://www.postgresql.org/docs/current/libpq-connect.html#id-1.7.3.8.3.6">string de conexão</a>.

Troque `db-name` pelo nome do banco de dados ao qual deseja utilizar em sua aplicação:

```bash
postgresql://admin:secret@localhost:5432/db-name
```