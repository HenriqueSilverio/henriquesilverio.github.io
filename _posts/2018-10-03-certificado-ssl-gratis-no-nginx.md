---
layout:     post
title:      Certificado SSL/TLS com Let’s Encrypt no Nginx
date:       2018-10-03 22:25:00
summary:    Passo a passo para gerar certificado SSL/TLS e configurar no Nginx.
categories: nginx
---

## Instalar o cliente do Let’s Encrypt

Primeiro adicione o repositório do **certbot** com o seguinte comando:

`add-apt-repository ppa:certbot/certbot`

Em seguida instale o **certbot** e o plugin para o Nginx:

`apt-get update`

`apt-get install python-certbot-nginx`

## Obter o certificado SSL/TLS

Para gerar o certificado com o plugin para o Nginx, basta rodar o comando:

`sudo certbot --nginx -d domain.com -d www.domain.com`

**Obs:** Substituindo `domain.com` pelo domínio da aplicação.

Após isso responda as perguntas que o assistente do **certbot** fará, e pronto!

O certificado será gerado, e terá validade de 90 dias.

## Renovar certificado automaticamente

Podemos configurar um cron job para renovar o certificado automaticamente.

Primeiro rode o comando:

`crontab -e`

E configure o comando do **certbot** para rodar diariamente:

`0 12 * * * /usr/bin/certbot renew --quiet`

Esse comando irá verificar a validade do certificado e renova-lo se necessário.

## Configuração necessária para utilizar Guzzle/cURL com SSL/TLS

Para que o Guzzle funcione corretamente em um ambiente com SSL/TLS, instale esse pacote:

`apt-get install ca-certificates`

Em seguida, no diretório do usuário que possui permissão de acesso aos projetos, crie o arquivo `~/.curlrc` com o seguinte código:

```
capath=/etc/ssl/certs/
cacert=/etc/ssl/certs/ca-certificates.crt
```

Reinicie o `php-fpm` e pronto! Problema resolvido.

Mais informações na [documentação do Guzzle](docs.guzzlephp.org/en/stable/request-options.html#verify-option).
