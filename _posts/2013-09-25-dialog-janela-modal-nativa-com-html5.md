---
layout:     post
title:      dialog - Janela modal nativa com HTML5
date:       2013-09-25 15:00:00
summary:
categories: html-e-css
---

Um recurso bastante utilizado em diversos tipos de aplicações são as famosas "janelas modais". Provavelmente você já deve ter utilizado esse recurso em algum de seus projetos. Caso já tenha utilizado, como você desenvolveu essa feature? Adicionou elementos extras no DOM e aplicou algumas técnicas de CSS? JavaScript "puro" ou talvez um plugin jQuery, certo?

A verdade é que existem "milhares" de técnicas para implementar uma janela modal. Mas em breve poderemos utilizar um elemento nativo do HTML5 para criar caixas de diálogo e janelas modais. Uma especificação do grupo <a href="http://www.whatwg.org/" target="_blank">WHATWG</a> está saindo do forno, e nos traz o novo elemento `dialog`. Nesse artigo, irei apresentar como ele funciona.

## Com vocês, o novo elemento dialog!

O elemento `dialog` representa uma parte da aplicação onde o usuário interage com a execução de uma tarefa, por exemplo uma caixa de diálogo ou uma janela modal. Esse elemento existe no DOM, e pode ser estilizado com CSS, assim como qualquer outro elemento de bloco.

Junto com este novo elemento, temos algumas APIs de JavaScript para manipular seus comportamentos, como por exemplo os métodos `.show()`, `.close()`, `.showModal()` e também o atributo `.returnValue`. E para personalizar a experiência de utilização temos o pseudo-elemento `::backdrop`, além de que a caixa/janela pode ser estilizada por CSS como já comentado.

Vamos criar então o nosso `dialog`:

{% highlight html %}
<dialog>
    <h3>Caixa de dialogo simples</h3>
    <p>Lorem ipsum dolor sit amet consectetur.</p>
    <button>Fechar</button>
</dialog>
<button>Abrir modal</button>
{% endhighlight %}

## Compatibilidade

O elemento `dialog` ainda está em processo de desenvolvimento e por enquanto não foi especificado como um padrão nos browsers. Em breve os navegadores modernos deverão passar a implementá-lo, mas até que isso aconteça, para testar essa feature, você pode usar o <a href="https://www.google.com/intl/pt-BR/chrome/browser/canary.html" target="_blank">Chrome Canary</a>, acessando `chrome://flags` e ativando os "recursos experimentais da plataforma Web".

![](/images/ativar-flag-experimental-web-platform.jpg)

Para os demais navegadores já existe também um fallback/polyfill criado pela equipe do Google Chrome. Você pode ver mais detalhes sobre como implementar esse fallback acessando o <a href="https://github.com/GoogleChrome/dialog-polyfill">repositório do projeto</a> no Github.

## API .show(), .close() e .returnValue

Para que nossa "caixa de diálogo" ou "janela modal" funcione, basta utilizarmos as novas APIs de JavcaScript. Um exemplo básico é feito utilizando os métodos `.show()` e `.close()`.

Como é de se esperar, quando o método `.show()` é chamado, ele checa se o elemento `dialog` já está sendo exibido, se já estiver, então nada acontece, caso contrário, ele adiciona um atributo `open` em nosso elemento `dialog` e exibe o mesmo para o usuário. É interessante notar que quando exibimos a "janela modal" através desse método `.show()`, o usuário ainda pode selecionar textos e interagir com os elementos da página que ficarão por trás dela.

E o método `.close()`? Se você adivinhar ganha um doce! <del>Tá você não vai ganhar um doce</del>, mas sim, o método `.close()` faz exatamente oque o nome sugere. Após chamar esse método, a nossa "janela modal" é fechada. Esse método também aceita um parâmetro opcional, que se for passado, é usado como valor de retorno e será gravado na propriedade `.returnValue`.

O código ficaria mais ou menos assim:

{% highlight javascript %}
var dialog = document.getElementById('my-dialog'),
    btOpen = document.getElementById('btn-open'),
    btClose = document.getElementById('btn-close');

btOpen.addEventListener('click' function() {
    dialog.show();
}, false);

btClose.addEventListener('click' function() {
    dialog.close();
}, false);
{% endhighlight %}

## API .showModal() e pseudo-elemento ::backdrop

Em alguns casos pode ser necessário "bloquear" o restante da página enquanto a "janela modal" estiver sendo exibida na tela. Para este efeito existe o método `.showModal()`. Basta chamar `.showModal()` ao invés de `.show()` para que a "janela modal" seja exibida na tela e o usuário não possa interagir com o restante do conteúdo enquanto não fechá-la.

{% highlight javascript %}
/* ... */

btOpen.addEventListener('click' function() {
    dialog.showModal();
}, false);

/* ... */
{% endhighlight %}

Muito legal não é mesmo? Mas ainda tem mais. Outra feature muito comum, é "escurecer" a página por trás da "janela modal", aplicando um background com um pouco de "transparência". Fazer isso é muito fácil: basta utilizar o pseudo-elemento `::backdrop` no CSS.

{% highlight css %}
dialog::backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
}
{% endhighlight %}

Espero que tenha gostado do artigo. Deixe suas opiniões nos comentários. =]
