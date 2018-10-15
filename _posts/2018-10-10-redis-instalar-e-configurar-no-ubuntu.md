---
layout:     post
title:      "Redis: Instalação e configuração"
date:       2018-10-10 11:25:00
summary:    Passo a passo para instalar e configurar o Redis em servidor Ubuntu.
categories: redis
---

## Pré-requisitos

Para instalar o Redis vamos precisar dos pacotes `build-essential` e `tcl`.

Instale os pacotes com o seguinte comando:

`sudo apt-get update`

`sudo apt-get install build-essential tcl`

## Instalação

Baixe a versão mais recente do Redis na pasta `/tmp`:

`cd /tmp`

`curl -O http://download.redis.io/redis-stable.tar.gz`

Extraia o pacote:

`tar xzvf redis-stable.tar.gz`

Compile:

`cd redis-stable`

`make`

Rode os testes unitários:

`make test`

E faça a instalação:

`sudo make install`

## Configuração

Crie um diretório de configuração padrão:

`sudo mkdir /etc/redis`

Copie o arquivo de configuração que veio com o fonte do Redis:

`sudo cp /tmp/redis-stable/redis.conf /etc/redis`

Abra o arquivo de configuração para fazer alguns ajustes:

`sudo nano /etc/redis/redis.conf`

Por padrão a diretiva `supervised`, virá com o valor `no`. Altere para `systemd`.

Na diretiva `dir`, informe um diretório para onde o Redis irá persistir dados.

Esse diretório deve ter permissões de escrita para o Redis. Faremos isso logo abaixo.

Exemplo:

`dir /var/lib/redis`

Salve e feche o arquivo.

## Permitir conexão externa

Para permitir conexões externas ao Redis, altere a diretiva `bind` no arquivo `/etc/redis/redis.conf`.

Por padrão, ela terá o valor `127.0.0.1`, mude para `0.0.0.0`.

### Restringir conexões de IPs desconhecidos

Por questões de segurança, devemos restrinjir conexões externas de IPs desconhecidos.

Para isso rode os seguintes comandos:

`sudo iptables -I INPUT -p tcp --dport 6379 -j DROP`

`sudo iptables -I INPUT -p tcp --dport 6379 -s 167.99.183.145 -j ACCEPT`

Nesse exemplo, apenas o IP `167.99.183.145` poderá se conectar ao servidor Redis da aplicação.

## Configurações do systemd

Crie um arquivo de configuração do systemd para o Redis:

`sudo nano /etc/systemd/system/redis.service`

Nesse arquivo, coloque o seguinte código:

```
[Unit]
Description=Redis In-Memory Data Store
After=network.target

[Service]
User=redis
Group=redis
ExecStart=/usr/local/bin/redis-server /etc/redis/redis.conf
ExecStop=/usr/local/bin/redis-cli shutdown
Restart=always

[Install]
WantedBy=multi-user.target
```

Salve e feche o arquivo.

## Criar usuário, grupo e diretórios

Crie um usuário e grupo chamado `redis`:

`sudo adduser --system --group --no-create-home redis`

Agora crie o diretório de persistência citado na passo anterior:

`sudo mkdir /var/lib/redis`

Ajuste as permissões desse diretório para o usuário e grupo `redis`:

`sudo chown redis:redis /var/lib/redis`

Restrinja as permissões para usuários comuns:

`sudo chmod 770 /var/lib/redis`

## Iniciar o Redis

Para iniciar o serviço do Redis com:

`sudo systemctl start redis`

E cheque se está tudo ok com:

`sudo systemctl status redis`

## Iniciando Redis no boot

Para iniciar o Redis com o boot do sistema, rode o comando:

`sudo systemctl enable redis`

Pronto!
