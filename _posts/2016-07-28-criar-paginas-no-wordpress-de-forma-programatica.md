---
layout:     post
title:      Criando páginas no WordPress de forma programática — aka "na unha"
date:       2016-07-28 20:40:00
summary: Nesse post mostro como criar páginas no WordPress de forma programática, ou "na unha", como costumam dizer por aí, e também como limpar os dados inseridos pelo plugin ao desinstalá-lo.
categories: wordpress
---

Caso você for desenvolver um plugin para WordPress, dependendo dos requisitos desse plugin, você provavelmente irá precisar criar algumas páginas automáticamente assim que o usuário instalá-lo ou em algum outro momento do programa.

Nesse post mostro **como criar páginas no WordPress de forma programática**, (ou "na unha", como costumam dizer por aí :-P), e também **como limpar os dados inseridos pelo plugin**, para que quando o usuário remover o plugin, ele não deixe "sujeira" no banco de dados.

## Criando página

Para criar uma página, basta usarmos a função `wp_insert_post`. Algo mais ou menos assim:

```php
function magic_page_install() {
    $page = array(
        'post_title'   => 'Magic Page',
        'post_content' => 'This page was created by Magic Page plugin!',
        'post_type'    => 'page',
        'post_status'  => 'publish'
    );

    $pageID = wp_insert_post($page);

    update_option('mpID', $pageID);
}

register_activation_hook(__FILE__, 'magic_page_install');
```

Note que pegamos o ID da página que foi criada e armazenamos em nosso banco de dados através da função `update_option`. Vamos precisar desse ID mais tarde.

## Enviando para a lixeira

Se o usuário desativar o plugin, vamos enviar a página que criamos anteriormente para a lixeira, mas sem excluí-la por completo, para que caso o usuário reative o plugin, possámos restaurá-la.

Para isso utilizamos a função `wp_delete_post`. O código fica mais ou menos assim:

```php
function magic_page_deactivate() {
    $pageID = get_option('mpID');
    wp_delete_post($pageID);
}

register_deactivation_hook(__FILE__, 'magic_page_deactivate');
```

Moleza né? Pegamos o ID da página que salvamos no passo anterior para podermos atualizá-la com a função `wp_delete_post`.

## Excluindo completamente

Bom, se o usuário for remover o plugin, então devemos excluir todos os dados previamente inseridos por ele, para que não fique "sujeira" indesejada no banco de dados que está sendo utilizado pelo WordPress.

Fazer isso, também é bem simples, veja:

```php
function magic_page_uninstall() {
    $pageID = get_option('mpID');
    delete_option('mpID');
    wp_delete_post($pageID, true);
}

register_uninstall_hook(__FILE__, 'magic_page_uninstall');
```

Deletamos o ID dá página que tinhámos armazenado, e novamente utilizamos a função `wp_delete_post`, mas dessa vez passamos um segundo argumento para ela, com o valor `true`. Dessa forma a página não será movida para a lixeira, e sim excluida completamente.

## Demonstração

Criei um plugin para poder testar o código mostrado neste artigo. Se quiser vê-lo funcionando, e dar uma olhada no código completo, você pode [baixá-lo aqui](https://github.com/HenriqueSilverio/magic-page). Qualquer dúvida, ou sugestão fique a vontade para deixar um comentário ou enviar um pull request.

### Referências:

<ul>
    <li><a target="_blank" href="https://developer.wordpress.org/reference/functions/wp_insert_post">wp_insert_post</a></li>
    <li><a target="_blank" href="https://codex.wordpress.org/Function_Reference/wp_delete_post">wp_delete_post</a></li>
    <li><a target="_blank" href="https://codex.wordpress.org/Function_Reference/wp_publish_post">wp_publish_post</a></li>
</ul>
