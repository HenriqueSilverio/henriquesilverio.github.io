---
layout:     post
title:      Internacionalização de JavaScript no WordPress
date:       2016-08-28 13:43:00
summary:    Aprenda como internacionalizar código JavaScript em seus projetos feitos com WordPress.
categories: wordpress
---

Atualmente estou desenvolvendo um plugin para WordPress com suporte completo para traduções. Fazer isso envolve vários fatores, coisas que dão assunto para outros posts e talvez eu até possa escrever mais sobre isso futuramente, mas neste artigo vou assumir que você já sabe **como usar JavaScript de forma correta no WordPress** e já conhece as **funções básicas para internacionalizar strings em plugins e temas**.

Um dos procedimentos envolvidos para que seus plugins e temas ofereçam suporte completo para traduções, é certificar-se de que as strings em seu código JavaScript também sejam traduzíveis. Nesse post vou te mostrar como fazer isso.

## Um exemplo prático

Em meu plugin estou usando um widget de <a target="_blank" href="http://www.erichynds.com/blog/jquery-ui-multiselect-widget">multiselect</a> para o jQuery UI, onde o usuário pode selecionar os serviços prestados por um determinado profissional. Algo mais ou menos assim:

![Meta box que precisa suportar tradução](/images/2016/08/meta_box_before_localize.png)

O JavaScript para montar esse widget seria algo do tipo:

```javascript
$('.has_widget_services').multiselect({
    checkAllText: 'Check all',
    uncheckAllText: 'Uncheck all'
});
```

Nesse caso, preciso dar um jeito para que as strings **Check all** e **Uncheck all** possam ser traduzidas. E agora? Como vamos fazer isso?

## Um truque chamado `wp_localize_script`

Resolver esse problema é bem simples. Para isso o WordPress nos oferece uma função chamada <a target="_blank" href="https://codex.wordpress.org/Function_Reference/wp_localize_script">`wp_localize_script()`</a>. Com essa função, após <a target="_blank" href="">registrar</a> ou <a target="_blank" href="https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts">enfileirar</a> nosso script, nós podemos configurar um array PHP que será passado para nosso JavaScript como um objeto simples. Confuso? Calma, na prática é muito mais simples do que parece.

O código PHP para isso seria mais ou menos assim:

```php
<?php

// 1. Em um array armazenamos os valores devidamente marcados para tradução.
$has_vars = array(
    'checkAllText'   => __( 'Check all', 'plugin-domain' ),
    'uncheckAllText' => __( 'Uncheck all', 'plugin-domain' )
);

// 2. Enfileiramos o nosso arquivo JavaScript.
wp_enqueue_script(
    'has-plugin',
    plugin_dir_url( __FILE__ ) . 'js/has-plugin.js',
    array( 'jquery-multiselect' ),
    1.0.0,
    true
);

// 3. Passamos os valores para a função `wp_localize_script()`.
wp_localize_script( 'has-plugin', 'hsaf_vars', $has_vars );
```

A função `wp_localize_script()` recebe 3 argumentos, que são:

1. `$handle`: O identificador do script a ser localizado.
2. `$name`: O nome da variável que irá ser usada no JavaScript.
3. `$data`: Os dados a serem passados para o JavaScript.

Viu que bacana? Com essa função podemos enviar dados do servidor para o JavaScript de forma "elegante" sem quebrar a <a target="_blank" href="https://www.profissionaisti.com.br/2015/06/entendendo-a-separacao-de-conceitos-separation-of-concerns-soc/">separação dos conceitos</a>, e dessa forma tornar nossas strings traduzíveis, com uma função como a <a target="_blank" href="https://codex.wordpress.org/Function_Reference/_2">__()</a> por exemplo.

Agora basta atualizar nosso JavaScript para pegar os dados passados na variável `hsaf_vars` criada pela função `wp_localize_script()`, da seguinte forma:

```javascript
$('.has_widget_services').multiselect({
    checkAllText: hsaf_vars.checkAllText,
    uncheckAllText: hsaf_vars.uncheckAllText
});
```

Pronto! Nosso widget já pode ser traduzido. =D E ficará assim:

![Meta box já traduzida para pt_BR](/images/2016/08/meta_box_after_localize.png)

Se você está começando pesquisar sobre internacionalização com WordPress agora, recomendo que dê uma estudada no "Plugin Handbook" pelo link que deixei logo abaixo.

Qualquer dúvida ou sugestão, fique a vontade para comentar.

### Referências:

<ul>
    <li><a target="_blank" href="https://developer.wordpress.org/plugins/internationalization">Plugin Handbook: Internationalization</a></li>
    <li><a target="_blank" href="https://codex.wordpress.org/Function_Reference/wp_localize_script">wp_localize_script()</a></li>
</ul>
