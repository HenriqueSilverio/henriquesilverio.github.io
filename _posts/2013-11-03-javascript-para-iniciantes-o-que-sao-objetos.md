---
layout:     post
title:      JavaScript para iniciantes - O que são Objetos?
date:       2013-11-03 19:44:00
summary:
categories: javascript-e-jquery
---

Escrevi este artigo com o objetivo de ajudar quem está começando estudar JavaScript. Como futuro programador JavaScript, é fundamental que você entenda o que são, e como funcionam os objetos nessa poderosa linguagem. É claro que existem muitos outros detalhes sobre Objetos em JavaScript, mas espero que esse artigo lhe sirva de ajuda como um ponto de partida em suas pesquisas.

## Let's go! O que são Objetos?

Objetos são como uma espécie de "super variáveis" que armazenam uma "coleção de valores" referenciados por nome, e que podem ser recuperados para serem utilizados em diversas outras partes de um programa. Em JavaScript praticamente qualquer tipo de dado é um objeto.

Cada item dessa "coleção de valores", é chamado de *propriedade*. Cada propriedade é composta por um par de "nome: valor". Quando uma propriedade armazena uma **função**, ela se torna o que chamamos de *método*.

## Criando objetos

Agora que já sabemos o que são objetos, vamos ver um pouco sobre como trabalhar com eles. Primeiramente vamos conhecer duas maneiras de se criar objetos.

#### Notação literal

A maneira mais simples (e recomendável) de se criar objetos em JavaScript é usando o que chamamos de *notação literal*. Um objeto literal é composto por um par de chaves "`{ }`", que envolve uma ou mais propriedades. Cada propriedade segue o formato "`nome: valor`" e devem ser separadas por vírgula.

Para entender bem, nada melhor que um exemplo. Imagine que você vai criar um programa para organizar álbuns de vários cantores e bandas. Aqui vamos criar um objeto para armazenar informações sobre um álbum da banda Metallica, depois você pode praticar criando objetos com suas bandas favoritas. Então, mãos a obra!

{% highlight javascript %}
var album = {
    title: "Metallica (Black Album)",
    released: 1991,
    showInfo: function() {
        alert("Titulo do album: " + this.title + "Lancado em: " + this.released);
    }
};
{% endhighlight %}

Conseguiu entender o que o código acima faz? Veja, é bem simples: primeiro criamos uma variável chamada "album". Depois criamos um objeto - note a abertura e fechamento das chaves: `{` e `}`. Então adicionamos duas propriedades e um método ao nosso objeto, que são: "title", "released" e "showInfo". Nas propriedades nós armazenamos o título e ano de lançamento do álbum, e no método temos uma função que irá exibir as informações sobre o álbum em uma "caixa de alerta" para o usuário. Mais fácil do que parece, não é mesmo?

#### Função construtora

Outra maneira de criar objetos em JavaScript é utilizando uma *função construtora*. Se quisermos criar o mesmo objeto que criamos anteriormente, só que usando uma função construtora para isso, basta escrever o seguinte código:

{% highlight javascript %}
var album = new Object();
    album.title = "Metallica (Black Album)";
    album.released = 1991;
    album.showInfo = function() {
    alert("Titulo do album: " + this.title + "Lancado em: " + this.released);
};
{% endhighlight %}

Como você pôde notar, a sintaxe ficou um pouco diferente. Aqui devemos utilizar a palavra-chave `new` seguida pela função construtora `Object()` ao invés de abrir e fechar chaves. Depois nós adicionamos as propriedades e métodos utilizando `album.title`, `album.released` e `album.showInfo` e atribuimos os valores à elas ao invés de colocar os pares de "nome: valor".

## Acessando propriedades e métodos

Após ter criado um objeto, você vai precisar acessar os valores que ele armazena. Podemos acessar (ou se preferir: "recuperar") os valores guardados em um objeto, de duas maneiras: utilizando *notação de ponto* ou *notação de colchetes*. Veja um exemplo:

{% highlight javascript %}
// notacao de ponto
album.title // Retorna: Metallica (Black Album)

// notacaoo de colchetes
album["title"] // Retorna: Metallica (Black Album)
{% endhighlight %}

Repare que no código acima, acessamos a mesma propriedade de duas maneiras diferentes. Geralmente é recomendável que você utilize a notação de ponto - `album.title` - por ser mais simples de ler e escrever.

Como os métodos são funções, você deve adicionar um par de parênteses - `()` - quando for acessá-los. Fora isso, nada de diferente. Veja no exemplo abaixo:

{% highlight javascript %}
// notacao de ponto
album.showInfo() // Exibe alerta:
 // Titulo do album: Metallica (Black Album) Lancado em: 1991

// notacao de colchetes
album["showInfo"]() // Exibe alerta:
 // Titulo do album: Metallica (Black Album) Lancado em: 1991
{% endhighlight %}

## Alterando e adicionando propriedades

#### Alterando

Vez por outra vamos precisar alterar os valores armazenados nas propriedades de nossos objetos. Fazer isso também é bem tranquilo. Basta acessar a propriedade que deseja alterar, utilizando a notação de ponto que acabamos de conhecer, e atribuir o novo valor à ela. Quer um exemplo?

{% highlight javascript %}
album.title = "Powerslave";
album.released = 1984;
{% endhighlight %}

O que aconteceu no código acima? Isso mesmo. Alteramos o título do álbum e o ano de lançamento. Agora nosso objeto armazena informações sobre um outro álbum de outra banda.

Para fixar, antes de prosseguir a leitura (supondo que você esteja lendo e digitando os códigos para treinar), altere os valores de `title` e `released` para Metallica (Black Album) e 1991 novamente.

#### Adicionando

Bom, agora que o título do nosso álbum voltou a ser "Metallica (Black Album)", que tal adicionar uma lista com os títulos das faixas do álbum? Sim, nós podemos adicionar novas propriedades e métodos aos nossos objetos mesmo após ter criado eles. A sintaxe é a mesma utilizada para alterar valores, que nós acabamos de ver.

Objetos podem armazenar qualquer tipo de dado válido em JavaScript, então, para criar uma lista com os títulos das faixas de nosso álbum, basta seguir o exemplo abaixo:

{% highlight javascript %}
// Aqui adicionamos um array com os nomes de algumas faixas do album.
// Para praticar voce pode adicionar todas as 12 faixas.
album.tracks = ["Enter Sandman", "Sad but True", "Holier Than Thou", "The Unforgiven"];
{% endhighlight %}

## Deletando propriedades

Você pode deletar uma propriedade ou método de um objeto utilizando o operador `delete` seguido pelo nome da propriedade. Vamos testar?

{% highlight javascript %}
typeof album.showInfo // "function"

delete album.showInfo // deleta o metodo showInfo

typeof album.showInfo // "undefined"
{% endhighlight %}

## Leitura adicional

Agora você já sabe o básico sobre objetos em JavaScript. Para uma abordagem mais profunda sobre o assunto, consultar **bons livros** pode ser de grande ajuda. Seguem algumas recomendações:

* "O Melhor do JavaScript", por Douglas Crockford. Capítulo 4, Página 26.
* "JavaScript - O Guia Definitivo" - 6ª Edição, por David Flanagan. Capítulo 6, Página 112.
