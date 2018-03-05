---
layout:     post
title:      Configurar Virtual Host no MAMP (servidor Apache)
date:       2018-03-05 20:35:00
summary:    Passo a passo para configurar Virtual Hosts na versão gratuita do MAMP.
categories: apache
---

Uma opção que tenho utilizado para trabalhar com a stack **Apache** / **MySQL** / **PHP** é o <a href="https://www.mamp.info" target="_blank">MAMP</a>.

E na versão gratuita do MAMP, infelizmente não tem uma solução "automática" para criar **Virtual Hosts** no Apache.

Então aqui vai um passo a passo sobre como fazer esse processo de forma manual.

## O arquivo `hosts`

Primeiro precisamos editar o arquivo `/private/etc/hosts`.

Adicione uma linha como essa (trocando `exemplo.dev` pelo endereço que você quiser usar):

```
127.0.0.1    exemplo.dev
```

Agora salve o arquivo, e digite a senha do seu Mac caso for solicitado.

Sempre que quiser criar um novo endereço, você deve repetir esse processo, adicionando-o no arquivo `hosts`.

## O arquivo `httpd.conf`

Na pasta `Applications/MAMP/conf/apache` você vai encontrar um arquivo chamado `httpd.conf`.

Abra esse arquivo e procure pelo seguinte trecho:

```
# Virtual Hosts
# Include /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf
```

Descomente a linha do `Include`. (Basta retirar o `#`).

## O arquivo `httpd-vhosts.conf`

Na pasta `Applications/MAMP/conf/apache/extra`, abra o arquivo `httpd-vhosts.conf`.

No final do arquivo, adicione o seguinte código:

```
<VirtualHost *:80>
    DocumentRoot /Applications/MAMP/htdocs
    ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "/Applications/MAMP/htdocs/exemplo.dev"
    ServerName exemplo.dev
</VirtualHost>
```

Salve e feche o arquivo. Reinicie o Apache, e pronto!

Seu Virtual Host está configurado, e você pode acessá-lo em: `http://exemplo.dev`.
