---
layout:     post
title:      JavaScript - Descobrir Menor e Maior valor em um Array
date:       2014-02-02 21:54:00
summary:
categories: javascript-e-jquery
permalink:  :categories/:title
---

<p>Neste artigo irei mostrar técnicas para resolver de forma muito simples, um problema que geralmente uma hora ou outra acabamos precisando solucionar (eu por exemplo, já me deparei com esse problema em uma entrevista de emprego). Essas técnicas podem não ser novidade para alguns, mas tenho certeza que poderá ser novidade (e de forte ajuda) para outros.</p>

<h3>O problema</h3>

<p>Digamos que você tenha um array com alguns números variados:</p>

```javascript
var random = [2, 3, 1, 4, 6, 5];
```

<p>Agora você precisa:</p>

<ul>
    <li>Encontrar o menor valor dentro do array.</li>
    <li>Encontrar o maior valor dentro do array.</li>
    <li>Descobrir o índice de um valor específico.</li>
</ul>

<p>E então, já sabe como fazer? Veja como é simples.</p>

<h3>Menor e maior valor dentro do array</h3>

<p>Olhando para o objeto <code>Math</code> nativo da linguagem JavaScript, podemos encontrar vários métodos úteis para realizar operações aritméticas mais complexas. Entre esses, temos os métodos <code>Math.min</code> e <code>Math.max</code>, que como você já deve ter imaginado, encontram respectivamente o menor e o maior valor entre um dado conjunto de números.</p>

<p>Maravilha! Problema resolvido. Será mesmo?</p>

<p>Bom, na verdade se você leu com atenção, deve ter notado que os métodos <code>Math.min</code> e <code>Math.max</code> encontram o menor e o maior valor entre um dado conjunto de <strong>números</strong>. Mas nós precisamos encontrar o menor e o maior valor de um <strong>array</strong>.</p>

<p>Vamos testar?</p>

<p>Abra o <a href="https://developers.google.com/chrome-developer-tools/" target="_blank">Chrome DevTools</a>, <a href="https://developer.mozilla.org/en-US/docs/Tools" target="_blank">Firefox Developer Tools</a>, <a href="https://getfirebug.com/" target="_blank">Firebug</a> ou qualquer outra ferramenta que você use para brincar com JavaScript, e digite o código abaixo:</p>

```javascript
Math.min( [1, 2, 3] ); // Retorna: NaN
Math.max( [1, 2, 3] ); // Retorna: NaN
```

<p>É, o resultado não foi o esperado. Mas isso pode ser resolvido com uma técnica bem simples.</p>

<p>O segredo da coisa é: podemos pegar funções que recebem um número indeterminado de argumentos (assim como <code>Math.min</code> e <code>Math.max</code>), e adaptá-las para serem utilizadas em um array, através do método <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply" target="_blank">.apply()</a>. Não faz parte desse artigo explicar como o método <code>.apply()</code> funciona, mas você pode clicar no link anterior para ler mais sobre o ele.</p>

<p>Sacou a ideia? Ainda não? Após ver o exemplo abaixo tudo ficará mais claro.</p>

```javascript
// Funcao para retornar o menor valor de um array
Array.min = function(array) {
    return Math.min.apply(Math, array);
};

// Funcao para retornar o maior valor de um array
Array.max = function(array) {
    return Math.max.apply(Math, array);
};

// Agora e so pegar os resultados
var random = [2, 3, 1, 4, 6, 5];  // Nosso array
console.log( Array.min(random) ); // Menor valor
console.log( Array.max(random) ); // Maior valor
```

<p>Ótimo! Agora sim temos boa parte do nosso problema resolvido.</p>

<p>Bom, em alguns casos você pode também receber um array que possui índices vazios ou que não possuem valores numéricos. Se esse for o seu caso, também é possível utilizar a técnica mostrada acima, basta fazer alguns ajustes para verificar os valores contidos no array antes de passá-lo como argumento para o método <code>.apply()</code>. Fazer essas verificações já foge do escopo desse artigo, mas caso você precise de ajuda para fazer isso, deixe um comentário abaixo.</p>

<h3>Bônus: Descobrir o índice (posição) de um valor específico</h3>

<p>Para finalizar, precisamos descobrir o índice (posição) de um dado valor específico dentro do nosso array.</p>

<p>Graças ao método nativo <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf" target="_blank">.indexOf()</a>, fazer isso é muito, mas muito fácil. Basta digitar o seguinte código:</p>

```javascript
var random = [2, 3, 1, 4, 6, 5];  // Nosso array
console.log( random.indexOf(1) ); // Retorna a posicaoo do numero 1 no array
```

<p>Pronto! Agora nosso problema foi resolvido por completo.</p>

<h4>Referências</h4>

<ul>
    <li><a href="http://ejohn.org/blog/fast-javascript-maxmin/" target="_blank">Fast JavaScript Max/Min</a></li>
    <li><a href="http://aaroncrane.co.uk/2008/11/javascript_max_api/" target="_blank">Math.max in JavaScript</a></li>
    <li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply" target="_blank">Function.prototype.apply()</a></li>
    <li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf" target="_blank">Array.prototype.indexOf()</a></li>
</ul>
