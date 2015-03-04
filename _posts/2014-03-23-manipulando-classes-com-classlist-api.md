---
layout:     post
title:      Manipulando classes com classList API
date:       2014-03-23 22:54:00
summary:
categories: javascript-e-jquery
permalink:  /:categories/:title
---

<p>Manipular classes de CSS em elementos HTML é uma tarefa muito útil, e até corriqueira, para quem trabalha com JavaScript. Provavelmente, você já sabe como fazer isso com jQuery. Porém, o que nem todos sabem ainda, é que temos uma API nativa de JavaScript para executar essas tarefas.</p>

<p>Neste artigo vou lhe apresentar a <a href="https://developer.mozilla.org/en-US/docs/Web/API/Element.classList" target="_blank">classList API</a>. Essa API é bem simples de ser utilizada, e é extremamente útil para diversas "brincadeiras".</p>

<p>Se você ainda não a conhece, verá que não é nada complicado manipular elementos dessa forma, mesmo sem utilizar bibliotecas como jQuery. Por outro lado, se você é um desenvolvedor experiente que já utiliza essa API no dia a dia, fique a vontade para deixar críticas e sugestões através dos comentários.</p>

<h3>Entendendo a API</h3>

Todo objeto <code>Element</code> possui um objeto <code>classList</code> que retorna um <a href="https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList" target="_blank">DOMTokenList</a> representando seu atributo <code>class</code> definido no documento HTML. O objeto <code>classList</code> possui uma propriedade <code>length</code> e é somente para leitura, porém podemos modificá-lo através de seus métodos, como <code>add</code> e <code>remove</code>. É aí que as coisas ficam interessantes.

Os métodos disponíveis em <code>classList</code> são:

<ul>
<li><strong>add</strong></li>
<li><strong>remove</strong></li>
<li><strong>toggle</strong></li>
<li><strong>contains</strong></li>
</ul>

<p>Vamos considerar agora cada um desses métodos.</p>

<h3>Adicionando classes com classList.add</h3>

<p>Para adicionar uma ou mais classes em um elemento HTML, basta selecioná-lo e chamar o método <code>classList.add</code>, passando uma <code>String</code> como argumento. É interessante notar que podemos adicionar multiplas classes de uma só vez. Para isso, informe os nomes das classes que deseja adicionar separados por vírgula. Exemplo:</p>

```javascript
// Selecionamos um elemento span no DOM:
var mySpan = document.querySelector( 'span' );

// Agora adicionamos a classe highlight para destaca-lo:
mySpan.classList.add( 'highlight' );

// Agora adicionamos mais 3 classes de uma so vez:
mySpan.classList.add( 'feature', 'label', 'label-primary' );
```

<h3>Removendo classes com classList.remove</h3>

<p>Além de adicionar novas classes, vez por outra você vai precisar também remover classes já existentes. Para isso, temos o método <code>classList.remove</code>. Vale notar, que assim como o método <code>add</code>, podemos remover multiplas classes de uma só vez. Exemplo:</p>

```javascript
// Selecionamos um elemento div no DOM:
var myDiv = document.querySelector( 'div' );

// Supondo que esse div tenha a classe 'foo', 'bar' e 'baz',
// vamos remover a classe 'baz':
myDiv.classList.remove( 'baz' );

// Agora vamos remover as classes 'foo' e 'bar' ao mesmo tempo:
myDiv.classList.remove( 'foo', 'bar' );
```

<h3>Alternando classes com classList.toggle</h3>

<p>Para dar um comportamento mais dinâmico em nossa interface, pode ser interessante alternar (inserir e remover) uma classe, respondendo a um clique, toque na tela ou outro evento. Com isso, podemos fazer coisas como por exemplo exibir/ocultar um bloco de conteúdo, exibir/ocultar um menu, destacar/remover destaque de um elemento, entre várias outras coisas.</p>

<p>É aí que o método <code>toggle</code> entra em ação. Passamos o nome de uma classe para o método <code>toggle</code>, e ele fica responsável por checar se um elemento tem ou não essa classe. Se já tiver: ele remove, se não tiver: ele adiciona. Tudo "automagicamente" sem precisar escrever instruções <code>if/else</code>, expressões regulares ou coisa do tipo.</p>

<p>Para ver o método <code>toggle</code> funcionando, o ideal é registrarmos uma rotina de tratamento de eventos como comentei acima. No final do artigo, você encontra um exemplo assim. Mas a sintaxe desse método é a seguinte:</p>

```javascript
// Alterna a classe 'is-visible' no elemento 'myDiv':
myDiv.classList.toggle( 'is-visible' );
```

<h3>Verificando classes com classList.contains</h3>

<p>Talvez você precise checar se um elemento possui determinada classe e dependendo do resultado, executar uma ou outra tarefa. Se esse for o caso, utilize o método <code>classList.contains</code>. Exemplo:</p>

```javascript
if( myDiv.classList.contains( 'is-visible' ) ) {
    // Se o elemento 'myDiv' possui a classe 'is-visible':
    // Faca alguma coisa interessante aqui.
} else {
    // Se nao...
    // Faca alguma outra coisa aqui.
}
```

<h3>Exemplo dinâmico</h3>

<p>Para que você possa visualizar melhor as coisas, fiz um exemplo bem simples onde você pode interagir com a <strong>classList API</strong> clicando nos botões. Ao testar o botão <code>contains</code>, repare a saída gerada no console.</p>

<a class="jsbin-embed" href="http://jsbin.com/mafix/1/embed?js,console,output">classList API</a><script src="http://static.jsbin.com/js/embed.js"></script>

<h3>Compatibilidade nos browsers</h3>

<p>Ao aplicarmos a <strong>classList API</strong> (ou qualquer outro recurso) em nossos projetos, é sempre bom ficar atento em relação a quais browsers suportam ou não tal API ou recurso que queremos implementar, e então tomar as decisões corretas.</p>

<p>Para isso, gosto bastante do site <a href="http://caniuse.com/" target="_blank">Can I use</a>.</p>

<p>Como podemos ver na tabela abaixo, o suporte à <strong>classList API</strong> é bem tranquilo em vários navegadores. Para variar um pouco, no IE só funciona a partir da versão 10+. Mas isso não é nenhuma surpresa né? :-P.</p>

<a href="http://caniuse.com/classlist" target="_blank">
    <img src="/images/browser-support-table.jpg" alt="Can I Use classList API">
</a>

<p>Mas fique tranquilo. Qualquer browser moderno aceita essa API, e se você precisa dar suporte aos navegadores mais antigos, pode usar algum <a href="http://en.wikipedia.org/wiki/Polyfill" target="_blank">polyfill</a> disponível na Internet. Um deles você encontra na <a href="https://developer.mozilla.org/en-US/docs/Web/API/Element.classList" target="_blank">documentação da Mozilla Developer Network</a>.</p>

<h3>Conclusão</h3>

<p>Agora você já sabe como manipular classes em seus documentos HTML de maneira muito fácil e sem depender de bibliotecas de terceiros. O suporte à essa API é muito bom em todos os browsers modernos e podemos utilizar um polyfill para os que não oferecem suporte. API's nativas podem facilitar bastante nossa vida como desenvolvedores Web, basta conhece-las e colocar em prática.</p>

<h3>Referências:</h3>

<ul>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Element.classList" target="_blank">classList</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList" target="_blank">DOMTokenList</a></li>
<li><a href="http://caniuse.com/classlist" target="_blank">Can I use classList?</a></li>
</ul>
