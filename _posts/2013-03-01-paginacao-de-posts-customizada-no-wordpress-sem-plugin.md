---
layout:     post
title:      Paginação de posts customizada no WordPress sem plugin
date:       2013-03-01 18:15:00
summary:    Aprenda fazer uma páginação de posts customizada para WordPress, sem utilizar um plugin.
categories: php-e-wordpress
---

Já faz alguns anos que adotei o [WordPress](http://br.wordpress.org) como plataforma de **CMS** para grande parte de meus projetos sejam eles blogs, sites institucionais etc. O **WordPress** é uma excelente plataforma de código open source mantida por uma comunidade enorme de desenvolvedores ao redor do mundo, possui [milhares de plugins](http://wordpress.org/extend/plugins) interessantes e podemos customiza-lo livremente de diversas maneiras. Por esses e outros motivos, trabalhar com **WordPress** é muito bacana.

Por padrão, o **WordPress** possui apenas os links “Próxima página” e “Página anterior” para navegar entre as páginas de posts de um blog. Isso pode ser ruim caso você tenha um blog com muitos artigos, pois torna a navegação cansativa. Por isso é recomendado que você substitua esses links de navegação por uma páginação de posts personalizada.

Nesse artigo, irei mostrar uma função interessante que lhe permitirá criar essa páginação de posts customizada sem utilizar um plugin para isso. Adaptei o script postado originalmente no site [Kriesi](http://www.kriesi.at/archives/how-to-build-a-wordpress-post-pagination-without-plugin#top), modificando o output do **HTML** gerado, e estilizando os links com o **Twitter Bootstrap**.

Veja o [código fonte no Github](https://github.com/HenriqueSilverio/exemplos-blog/blob/master/wp-custom-pagination/functions.php).

## Explicação passo a passo

Primeiramente, dentro do nosso arquivo **functions.php** criamos uma função chamada `custom_pagination` passando dois parâmetros opcionais para ela. O primeiro parâmetro iremos utilizar mais tarde para chamar nossa paginação em um loop personalizado, e o segundo parâmetro é um número usado para determinar a quantidade de links que irão aparecer antes das setas indicando para “avançar” para próxima e última página. Se você ainda não tem um arquivo functions.php no diretório raiz do seu theme, crie um e adicione o código abaixo:

{% highlight php %}
<?php

function custom_pagination($pages = '', $range = 2){
    // o restante do codigo sera inserido aqui
}

?>
{% endhighlight %}

Feito isso, nós iremos armazenar o número máximo de itens a serem exibidos em uma váriavel, para podermos realizar alguns cálculos com maior facilidade mais tarde.

{% highlight php %}
<?php $showitems = ($range * 2) + 1; ?>
{% endhighlight %}

A seguir nós precisamos acessar a váriavel global **$paged**. O **WordPress** utiliza essa váriavel para armazenar qual é a página atual que você está visualizando. Se essa váriavel estiver vazia, então nós setamos seu valor para 1. Fazemos isso para remover o link no botão referente à página atual e exibi-lo como “ativo”.

{% highlight php %}
<?php

global $paged;
if(empty($paged)) $paged = 1;

?>
{% endhighlight %}

Agora já sabemos qual página está sendo visualizada, mas também precisamos saber a quantidade total de páginas a serem listadas. Assumindo que **não estamos utilizando** um loop personalizado e que a váriavel **$pages** (não confunda com a váriavel **$paged**) não foi definida quando chamamos o script, podemos então utilizar outra váriavel global para obter esse número:

{% highlight php %}
<?php

if($pages == '') {
    global $wp_query;
    $pages = $wp_query->max_num_pages;
    if(!$pages) {
        $pages = 1;
    }
}

?>
{% endhighlight %}

Como você pode ver no código abaixo, usaremos um pouco de lógica e uma única função específica do **WordPress** chamada `get_pagenum_link()`. Com a função `get_pagenum_link()` nós podemos buscar a URL de uma página do **WordPress**. Passando o número da página como parâmetro nessa função: `get_pagenum_link(2)`, irá retornar o link para a página 2 do blog.

Primeiro nós checamos se o número de páginas é maior que 1 e se for, passamos a checar outros itens necessários antes de recuperar e exibir os resultados. Como o nosso foco é no Front-end, não entro em detalhes sobre essa programação, mas você pode estudar o código a vontade e entender mais profundamente o funcionamento da coisa toda.


{% highlight php %}
<?php

if(1 != $pages) {
    echo "<nav class='btn-group paginator'>";
    if($paged > 2 && $paged > $range+1 && $showitems < $pages) echo "<a href='".get_pagenum_link(1)."' class='btn'>Primeira</a>";
    if($paged > 1 && $showitems < $pages) echo "<a href='".get_pagenum_link($paged - 1)."' class='btn'>&lsaquo;</a>";

    for ($i=1; $i <= $pages; $i++) {
        if (1 != $pages &&( !($i >= $paged+$range+1 || $i <= $paged-$range-1) || $pages <= $showitems )) {
            echo ($paged == $i)? "<a class='btn current'>".$i."</a>":"<a href='".get_pagenum_link($i)."' class='btn' >".$i."</a>";
        }
    }

    if ($paged < $pages && $showitems < $pages) echo "<a href='".get_pagenum_link($paged + 1)."' class='btn'>&rsaquo;</a>";
    if ($paged < $pages-1 &&  $paged+$range-1 < $pages && $showitems < $pages) echo "<a href='".get_pagenum_link($pages)."' class='btn'>Ultima</a>";
    echo "</nav>\n";
}

?>
{% endhighlight %}

## O CSS

Para que nossa paginação fique mais interessante, podemos personalizar o **CSS** da maneira que acharmos melhor. Em meu exemplo de paginação eu adicionei as classes do **Twitter Bootstrap**, portanto o output **HTML** gerado pela função ficou dessa forma:


{% highlight html %}
<nav class='btn-group paginator'>
    <span class='btn current'>1</span>
    <a class='btn' href="http://blog/page/2">2</a>
    <a class='btn' href="http://blog/page/3">3</a>
    <a class='btn' href="http://blog/page/2">&rsaquo;</a>
    <a class='btn' href="http://blog/page/12">&raquo;</a>
</nav>
{% endhighlight %}

Para que tudo fique bonito conforme eu queria, precisei dos componentes “Buttons” e “Button groups and dropdowns” do **Twitter Bootstrap** e dos estilos **CSS** abaixo. Mas você pode ficar a vontade para personalizar sua paginação como bem entender, criando novos estilos ou até mesmo alterando as classes no output da função. Aí é com você!

{% highlight css %}
.current {
    color: #333;
    background-color: #e6e6e6;
    *background-color: #d9d9d9;
    background-image: none;
    outline: 0;
    -webkit-box-shadow: inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);
       -moz-box-shadow: inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);
            box-shadow: inset 0 2px 4px rgba(0,0,0,.15), 0 1px 2px rgba(0,0,0,.05);
}
{% endhighlight %}

Nossa paginação está pronta e para exibi-la em seu blog basta chamar a função em seu template do seguinte modo:


{% highlight php %}
<?php custom_pagination(); ?>
{% endhighlight %}

## Paginção com loop personalizado

Provavelmente em algumas ocasiões você irá precisar chamar uma paginção de posts em um loop personalizado. Esse loop personalizado não é armazenado por padrão na váriavel global **$wp_query**, então nós fazemos isso adicionando o seguinte código:

{% highlight php %}
<?php $pages = $wp_query->max_num_pages; ?>
{% endhighlight %}

Nesse caso você vai precisar chamar a função `custom_pagination()` setando o primeiro parâmetro com o seu loop personalizado. Seria algo mais ou menos assim:

{% highlight php %}
<?php custom_pagination($nome_do_loop->max_num_pages); ?>
{% endhighlight %}

Se você precisa entender melhor como funciona um **loop personalizado**, comece lendo o artigo “[Customizando a query do WordPress](http://wpmidia.com.br/tutoriais/customizando-query-wordpress/)” postado pela amiga [Miriam](https://twitter.com/miriamdepaula) e outros links que deixo aqui abaixo:


* [Codex – The loop](http://codex.wordpress.org/The_Loop)
* [Codex – Query posts](http://codex.wordpress.org/Template_Tags/query_posts)
* [Rockin’ out WordPress custom loops](http://www.kristarella.com/2010/02/wordpress-custom-loops)
