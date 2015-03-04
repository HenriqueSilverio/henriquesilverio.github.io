---
layout:     post
title:      Font Icons para Custom Post Types e Temas ~ WordPress 3.8
date:       2014-01-09 11:27:00
summary:
categories: php-e-wordpress
permalink:  /:categories/:title
---

<p>Se você conhece o WordPress há um bom tempo e tem acompanhado de perto sua evolução, ao instalar a versão 3.8, sem dúvida deve ter se surpreendido com a grande mudança feita na interface do painel administrativo. O design ficou muito mais limpo e moderno, coisa linda.</p>

<p>Entre as várias mudanças que ocorreram, uma delas é que agora foram adicionados Font Icons (chamados de Dashicons) no lugar das imagens que eram usadas anteriormente. Os ícones seguem um estilo flat, e combinam muito bem com o novo estilo dado à dashboard, e trazem vários benefícios, como por exemplo: são preparados para as poderosas telas de retina.</p>

<p>Bom, após conhecer os novos ícones, é claro que você vai querer utilizá-los ao desenvolver seus plugins e temas. Neste artigo, trago uma dica rápida para você que deseja fazer isso. Veja como é bem tranquilo.</p>

<h3>Dashicons para Custom Post Types</h3>

<p>Um dos parâmetros que você deve informar ao <a target="_blank" href="http://codex.wordpress.org/Function_Reference/register_post_type">registrar um post type</a> é o <code>menu_icon</code>. E para inserir o Font Icon (Dashicon) que você desejar, basta informar o nome de sua respectiva classe CSS.</p>

<p>Para descobrir qual é o nome da classe CSS que corresponde ao ícone desejado, você pode acessar o link: <a href="http://melchoyce.github.io/dashicons/">melchoyce.github.io/dashicons/</a>. Nessa página você verá uma lista com todos os ícones disponíveis. Basta clicar no ícone para que ele seja selecionado e no topo do site você verá o nome da classe CSS, aí é só copiar esse nome e informá-lo ao parâmetro <code>menu_icon</code>.</p>

![Font Icon Dashicon WordPress 3.8](/images/Font-Icon-Dashicon-WordPress-3.8.jpg)

```php
<?php

register_post_type( 'lancamentos', array(
    // ...
    'menu_icon' => 'dashicons-list-view',
    // ...
) );
```

![Font Icons Painel WP](/images/Font-Icons-Painel-WP.jpg)

<h3>Dashicons para Temas no Front-End</h3>

<p>Se você deseja utilizar os novos ícones no Front-End de um tema, poderá fazer isso também de forma muito simples. Basta passar o <code>dashicons</code> como uma dependência de sua folha de estilos na chamada da função <code>wp_enqueue_style</code>, como no exemplo abaixo:</p>

```php
<?php

function my_theme_enqueue_style() {
    wp_enqueue_style(
        'my-theme-style',
        get_stylesheet_uri(),
        array( 'dashicons' )
    );
}

add_Action( 'wp_enqueue_scripts', 'my_theme_enqueue_style' );
```

<p>O código mostrado acima, irá se encarregar de chamar o CSS para os Dashicons sempre junto com o CSS do seu tema. Feito isso, basta voltar ao <a target="_blank" href="http://melchoyce.github.io/dashicons/">site do Dashicons</a>, clicar no ícone que deseja utilizar, e depois clicar em "Copy CSS" para obter o código referente ao ícone selecionado, como mostrado na figura abaixo:</p>

![Copy Font Icon CSS](/images/Copy-Font-Icon-CSS.jpg)

<p>Com o código do ícone em mãos, agora basta utilizá-lo em um pseudo-elemento <code>:before</code> ou <code>:after</code> no CSS do seu tema, seguindo o exemplo:</p>

```css
.my-item:before {
    content: "\f163";
    font-family: "dashicons";
}
```

<h2>Conclusão</h2>

<p>Não é de hoje que muitos encaram o WordPress como uma "espécie de framework" completo para desenvolver os mais diferentes tipos de aplicações Web. Neste artigo consideramos um recurso simples, mas que faz uma grande diferença na experiência do usuário, inclusive tornando seu tema ou plugin preparado para dispositivos com telas de alta definição. E vimos como o WordPress lida com isso, tornando o processo de desenvolvimento bem mais tranquilo, mesmo nesses "pequenos detalhes".</p>

<p>Espero que essas informações lhe sejam úteis. Qualquer dúvida, crítica ou sugestão, é só deixar um comentário abaixo.</p>
