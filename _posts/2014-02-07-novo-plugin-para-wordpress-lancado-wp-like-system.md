---
layout:     post
title:      Novo plugin para WordPress lançado - WP Like System
date:       2014-02-07 11:52:00
summary:
categories: php-e-wordpress
---

É com grande satisfação que venho através desse post, anunciar mais um novo plugin que desenvolvi para WordPress. O nome desse plugin é <strong>WP Like System</strong>, e você pode fazer o <a href="http://wordpress.org/plugins/wp-like-system/" target="_blank">download aqui</a> no repositório oficial do WordPress.org.

<h3>O que esse plugin faz?</h3>

O <strong>WP Like System</strong> adiciona um sistema de 'curtir', semelhante ao famoso recurso lançado pelo Facebook. Dessa forma, os usuários podem avaliar seus posts e interagir com seu site/blog, mas sem precisar estar logado na rede social, e não é necessário fazer integração com scripts de terceiros, pois as avaliações dos usuários ficam armazenadas em sua própria base de dados.

<h3>Principais recursos</h3>

<ul>
    <li><strong>Opções "Curtir" e "Desfazer".</strong></li>
    <li><strong>Exibe total de pessoas que já curtiram.</strong></li>
    <li><strong>Fácil de usar:</strong> Nada de configurações complicadas e desnecessárias. Basta instalar, colar o snippet do plugin dentro do loop do seu tema, e tudo funciona como o esperado.</strong></li>
    <li><strong>Fácil de personalizar:</strong> marcação HTML limpa e com classes CSS para que você possa estilizar a aparência do plugin da forma que achar melhor, caso ache necessário.</li>
    <li><strong>Pronto para traduções</strong> e já está disponível nos idiomas Português e Inglês.</li>
</ul>

<h3>Como instalar</h3>

O processo de instalação é feito como qualquer outro plugin para WordPress.

Após ter instalado, abra o arquivo <code>content.php</code> ou <code>single.php</code> do seu tema e cole o seguinte snippet dentro do loop:

```php
<?php

    if( function_exists( 'has_wpls_show_likes' ) ) {
        has_wpls_show_likes( get_the_ID() );
    }

?>
```

Qualquer dúvida, fique a vontade para <a href="http://wordpress.org/support/plugin/wp-like-system" target="_blank">abrir um tópico no fórum de suporte</a>.

<h3>Screenshots</h3>

Abaixo você pode ver algumas imagens que demonstram como o plugin funciona.

<a target="_blank" href="/images/screenshot-1.png">
    <img src="/images/screenshot-1.png" alt="WP Like System 1">
</a>

<a target="_blank" href="/images/screenshot-2.png">
    <img src="/images/screenshot-2.png" alt="WP Like System 2">
</a>

<a target="_blank" href="/images/screenshot-3.png">
    <img src="/images/screenshot-3.png" alt="WP Like System 3">
</a>

<h3>Gostou? Colabore.</h3>

Se você não é um programador, pode contribuir com o desenvolvimento do plugin por fazer um review lá no <a href="http://wordpress.org/plugins/wp-like-system/" target="_blank">repositório do WordPress.org</a> e deixar uma avaliação com 5 estrelas. Fazer isso não leva mais do que 3 minutos, não lhe custará nada, e irá me ajudar a manter esse plugin, bem como me incentivar a desenvolver outros plugins novos futuramente.

Se você é programador, o código fonte está disponível <a href="https://github.com/HenriqueSilverio/wp-like-system" target="_blank">nesse repositório no Github</a>. Fique a vontade para fazer um fork, e ajudar a melhorar o plugin.
