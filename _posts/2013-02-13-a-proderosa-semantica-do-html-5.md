---
layout:     post
title:      A poderosa semântica do HTML5
date:       2013-02-13 11:30:00
summary:    Um pouco sobre as novas tags semânticas do HTML5 que você deve usar já.
categories: html-e-css
permalink:  /:categories/:title
---

Cada vez mais desenvolvedores ao redor do mundo utilizam **HTML5** como linguagem de marcação padrão em seus projetos. Para falar a verdade, se você é um profissional da web e em pleno 2013 ainda não utiliza **HTML5**… “em que mundo você está?”

Já não restam mais dúvidas que o **HTML5** veio para nos ajudar a construir uma web melhor e mais acessível para todos. E nesse artigo mostro um dos aspectos que mais me chama atenção nesse assunto: **A poderosa semântica do HTML5**.

## Um breve relato sobre semântica

Você sabe o que é semântica? Certo dicionário define a palavra semântica da seguinte maneira:

> “Lingüística Ciência empírica, descritiva, que tem por objeto o estudo da relação dos signos com aquilo que eles significam, numa língua dada, i.e., estudo das palavras no que respeita a seus significados.”

Ta legal, mas e o que o HTML tem a ver com isso? Tudo.

O próprio nome HyperText Markup Language (em português Linguagem de Marcação de Hipertexto), mais conhecida por sua sigla HTML, já diz tudo. A linguagem HTML é composta por diversas tags que são utilizadas para organizar e dar significado à informações na web de maneira não linear. Cada tag utilizada na marcação carrega com sigo mesma um significado, e é esse significado que será transmitido para os diversos meios de acesso como robôs de busca, leitores de telas entre outros dispositivos.

Buscando aplicações ricas em significado, nós temos feito uso de tags como por exemplo `<h1>` para marcar um título de grande importância no documento, ou um `<h2>…<h6>` para títulos de menor importância, `<p>` para mostrar que determinado texto compõe um parágrafo e assim por diante. Isso é muito legal, pois torna o documento mais acessível.

Mas e quando você precisa marcar um bloco de conteúdo referente ao cabeçalho da página? Ou que tag você utiliza para criar uma barra de navegação, uma sidebar, o conteúdo de um artigo postado, ou o rodapé de um site por exemplo? Faria como no exemplo abaixo?

![Exemplo 1: Estrutura com div's](/images/html-5-exemplo-01.jpg)

{% highlight html %}
<div class="header">
    <p>div.header</p>
</div>

<div class="nav">
    <p>div.nav</p>
</div>

<div class="sidebar">
    <p>div.sidebar</p>
</div>

<div class="container">
    <p>div.container</p>
    <div class="post">
        <p>div.post</p>
    </div>
</div>

<div class="footer">
    <p>div.footer</p>
</div>
{% endhighlight %}

Essa é uma estrutura básica e utilizada durante muito tempo por muitos desenvolvedores. Mas você já parou para pensar qual é o valor semântico do seu código escrito assim?

<blockquote>
    <p>“The div element represents nothing at all. It can be used with the class, lang/xml:lang, and title attributes to mark up semantics common to a group of consecutive elements”</p>
    <footer>
        <cite>Fonte: <a target="_blank" href="http://dev.w3.org/html5/html-author/#the-div-element">http://dev.w3.org/html5/html-author/#the-div-element</a></cite>
    </footer>
</blockquote>

Conforme diz a documentação oficial feita pelo **W3C**, a tag `<div>` não possui nenhum valor semântico… simplesmente é utilizada para dividir o documento em blocos. Blocos que não significam nada. Triste situação a nossa… Como assim marcar partes tão importantes de nossas aplicações atribuindo a elas algo que lhes deixa sem valor algum? Isso está muito errado.

Mas é aí que o **HTML5** começa ficar interessante e nos mostra o quanto é poderoso!

## Novas tags e uma semântica rica

Antes de mais nada, sem muitas explicações, apenas veja como ficou nossa estrutura anterior feita com os novos elementos do **HTML5**.

![Exemplo 2: Estrutura semântica com HTML5](/images/html-5-exemplo-02.jpg)

{% highlight html %}
<header>
    <p>header</p>
</header>

<nav>
    <p>nav</p>
</nav>

<aside>
    <p>aside</p>
</aside>

<section>
    <p>section</p>
    <article>
        <p>article</p>
    </article>
</section>

<footer>
    <p>footer</p>
</footer>
{% endhighlight %}

De modo geral, as tags mostradas em nosso exemplo são auto explicativas. Nesse artigo não entro em detalhes sobre o significado e modo correto de se utilizar cada uma delas individualmente, mas em breve estarei escrevendo novos posts sobre isso aqui no blog.

É muito fácil notar a diferença não é mesmo? Agora sim estamos dando real significado ao nosso documento. As **novas tags do HTML5** como `<header>`, `<aside>`, `<section>`, `<article>` e `<footer>` mostradas em nosso exemplo, trazem uma semântica muito mais rica para utilizarmos em nossa marcação HTML. Com isso nosso conteúdo fica muito mais fácil de ser acessado por robôs de busca como o Google, ou leitores de tela para pessoas que possuem algum tipo de deficiência seja ela temporária ou não. Acessibilidade++

Tudo isso sem falar sobre os novos **data attributes**, **microformats**, **WAI-ARIA** e outros novos aspectos muito interessantes do **HTML5** que também serão assuntos para futuros artigos.

<a target="_blank" href="http://labs.henriquesilverio.com/novas-tags-html5/">Exemplos utilizados no artigo</a> | <a target="_blank" href="https://github.com/HenriqueSilverio/exemplos-blog/tree/master/novas-tags-html5">Código fonte no Github</a>

Semântica, acessibilidade, boas práticas de desenvolvimento, entre outros assuntos relacionados ao universo dos desenvolvedores front-ends serão sempre assuntos que estarei abordando por aqui. Espero que tenha gostado do artigo. Fique a vontade para deixar suas opiniões, dicas, elogios e sugestões nos comentários.
