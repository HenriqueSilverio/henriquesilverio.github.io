---
layout:     post
title:      1ª Conferência CSS Brasil
date:       2015-05-14 21:25:00
summary: Dia 09 de Maio de 2015 aconteceu em São Paulo a 1ª Conferência CSS do Brasil. Tive a oportunidade de estar presente nesse grande evento, e neste artigo compartilho minhas anotações de tudo que rolou por lá.
categories: eventos
---

No Sábado, dia 09 de Maio de 2015, tive a oportunidade de estar presente na **1ª Conferência CSS Brasil**, que aconteceu em São Paulo. Como já era de se esperar, o evento foi recheado de conteúdo muito bom.

Fiz algumas anotações e juntei tudo nesse artigo, para que você possa acompanhar e ficar por dentro do que rolou por lá.


## Credenciamento / Coffe

Cheguei no local por volta das 08h40min, estava rolando o credenciamento, um *coffe* esperto, e alguns stands de empresas parceiras do evento. Peguei meu crachá, fui na mesa do [Eu Compraria](http://eucompraria.com.br) e do [Stickers Devs](https://www.facebook.com/stickersdevs), não resisti e comprei uma camiseta de JavaScript e alguns adesivos muito legais! xD

<p style="text-align: center;">
    <img src="/images/camiseta-e-stickers.jpg" alt="Camiseta JavaScript e Stickers Devs">
</p>

## Abertura

A apresentação da conferência ficou por conta do [Daniel Filho](https://twitter.com/danielfilho). Para iniciar o evento, ele contou brevemente a história de como surgiu a ideia de um evento exclusivamente focado em CSS, e falou um pouco sobre os organizadores.

<p style="text-align: center;">
    <img src="/images/conferencia-css-2015.jpg" alt="Palco Conferência CSS Brasil 2015">
</p>


## Motions UI com CSS

**Slides:** [https://speakerdeck.com/zehfernandes/motion-u-dot-i-with-style](https://speakerdeck.com/zehfernandes/motion-u-dot-i-with-style)

Na primeira palestra do dia, o [Zeh Fernandes](https://twitter.com/zehf) falou sobre *motion UI* e animações com CSS.

Vimos uma linha do tempo sobre animações na Web, passando desde o inicio onde a famosa tag `blink` era muita utilizada, depois chegaram as animações feitas em Java, e a "era de ouro do Flash", até que o HTML5 e o CSS3 começaram ganhar espaço. Interessante notar que, nesse inicio da "era HTML5 e CSS3", existia uma grande tendência de querermos imitar os efeitos que antes eram criados com Flash.

Depois vimos que as animações devem ter um significado. Animações bem planejadas e executadas, facilitam a comunição do usuário com a interface e o conteúdo. Ajudam o cérebro a entender melhor o fluxo da informação, preenchendo *gaps* na interação do usuário com o conteúdo.

Foram apresentados diferentes tipos de animações, para:

* Chamar atenção, dizer ao usuário para "onde ir";
* Dar significado, contexto e/ou feedback;
* Reforçar a identidade da marca;
* Tornar a interface mais legal/divertida de se usar.

Uma frase interessante que foi citada: Animações são como a nova tipografia. Então pense antes de usar comic sans.

E por fim tivemos dicas de performance, boas práticas e uma demonstração de uso das novas ferramentas do Chrome DevTools para debugar animações. Sensacional.

E para fechar, a mensagem que fica é: animações devem ser planejadas desde o começo do projeto. E este é um processo que deve envolver também Web Designers e UI Designers, não são apenas **mais uma** responsabilidade única dos desenvolvedores Front-End.


## Dominando a tipografia na web

**Slides**: [http://www.slideshare.net/eshiota/dominating-the-web-typography](http://www.slideshare.net/eshiota/dominating-the-web-typography)

[Eduardo Shiota](http://twitter.com/shiota) mostrou que é importante entendermos a origem da tipografia para poder aplicá-la de forma correta na Web. Tivemos uma aula de história, vindo desde os tempos primitivos passando pela evolução da escrita dos antigos egípcios, gregos, a era da escrita gótica, e a famosa máquina de tipos de Gutenberg até os dias atuais.

Depois foi feita uma explicação sobre as diferentes categorias de fontes como as serifadas e as sem serifa, as góticas, cursivas, display, dingbats e font icons.

Fomos lembrados que se tratando de Web e a grande diversidade de dispositivos que temos hoje em dia, **[1px não é 1px](http://loopinfinito.com.br/2013/11/12/quanto-vale-1px)**, que é necessário **muito** teste e que tipografia muitas vezes é uma ciência subjetiva.

Então foram explicados os conceitos necessários para ter uma boa tipografia na Web, tais como qual medida escolhar: *px*, *em*, *rem*... tratar o *line-height*, e manter o rítmo de leitura com uma boa *baseline*.

E aí entra uma ideia chave: manter a harmonia é importante. Mas é impossível que tudo seja perfeito em **todos** os browsers, por isso *value perfect* > *pixel perfect*.

Então o Shiota apresentou algumas propriedades de CSS que até então não conhecia, como `font-kerning`, e como controlar algumas features de fonts *open-type* com `-webkit-font-feature-settings`. Muito show, animal.

A Web está cada vez mais sendo considerada uma fonte de conteúdo relevante. E o conteúdo é o que **realmente importa** para os usuários. Então saber escolher uma fonte descente é extremamente importante, mesmo que tenha que pagar "caro" por uma, duas ou a família inteira de fontes.


## Sorteio de brindes

Entre uma palestra e outra, tivemos vários sorteios de brindes. E não é que eu ganhei uma camiseta da conferência? E ainda acabei sendo sorteado duas vezes. Na segunda, que era uma cartela de adesivos, passei para outro participante, e daí pra frente quem ia sendo sorteado duas vezes também ia passando o brinde pra outro. Aqui está uma foto da camiseta, que foi aprovada pelo [Edu Agni](https://twitter.com/eduagni) (quem esteve presente vai entender isso melhor). :-P

<p style="text-align: center;">
    <img src="/images/camiseta-conferencia-css.jpg" alt="Camiseta da 1ª Conferência CSS BRasil">
</p>


## Testando seu CSS!

**Slides**: [https://speakerdeck.com/eduardojmatos/testes-de-css](https://speakerdeck.com/eduardojmatos/testes-de-css)

O [Eduardo Matos](https://twitter.com/eduardojmatos) mostrou que testar CSS também é coisa séria, e nos apresentou algumas ferramentas que estão disponíveis para fazermos isso.

Vimos que um teste **bom** deve ter boa performance, ser independente e usar o mínimo de recursos possível.

Hoje temos ferramentas que fazem desde um "simples" teste de sintaxe como [CSS Lint](https://github.com/CSSLint/csslint), ferramentas que geram estatística do código como [CSS Stats](http://cssstats.com/), até ferramentas para teste de regressão como [SUCSS](http://succss.ifzenelse.net/), [BackstopJS](https://github.com/garris/BackstopJS), entre outras.

Achei muito bacana essa ideia, mas acho que essas ferramentas ainda tem muito a amadurecer em comparação com as que temos para testar JavaScript. Enfim, é bom ficar atento no assunto.


## CSS Preprocessors: Sass 101

**Slides**: [http://pt.slideshare.net/loumontano/sass-conferencia-csssp](http://pt.slideshare.net/loumontano/sass-conferencia-csssp)

Diretamente da Argentina, a [Lourdes Montano](https://twitter.com/loumontano) veio para falar sobre Sass, e mandou muito bem.

Vários tópicos interessantes, falando desde como fazer a instalação do Sass, até sobre como usar placeholders, mixins, functions, criar uma boa estrutura de arquivos para organizar o projeto, e boas práticas para ter uma base de código manutenível e gerar um bom CSS no final.

Uma frase que ela disse e valeu tomar nota foi: "Sass te ajuda escrever CSS mais rápido, não melhor". Afirmando assim a importância de se saber realmente o que está fazendo, antes de sair escrevendo Sass por aí.


## The BGs

**Slides**: [http://pt.slideshare.net/bernarddeluna/the-bgs-background-css](http://pt.slideshare.net/bernarddeluna/the-bgs-background-css)

Com poucos slides e bastante *live coding*, a palestra do [Bernard de Luna]() foi muito criativa e inspiradora. Acho que a maioria não imaginava que essa única propriedade CSS - `background` - poderia render assunto para uma palestra inteira assim!

Bernard mostrou que o importante é fazer coisas que você ama. É necessário liberar a criatividade, não ter medo de errar para aprender, e que para fazer coisas que vão deixar outros surpresos nem sempre quer dizer que você tem que fazer algo extremamente complexo.

Um ponto legal que foi ressaltado, é a importância do **desenvolvedor CSS** no mercado. Outros podem se achar melhores que você só porque criam algorítmos com linguagens de Back-End, mas sempre ficarão surpresos se você mostrar o que é capaz de fazer "apenas com o simples" CSS. Então não se sinta o "patinho feio" da história. Valorize-se.

Para terminar, brincando com as propriedades `background`, `background-clip`, `linear-gradient` etc., ele criou uma tela com animações estilo discoteca, e ao som de Bee Gees todo mundo aplaudiu bastante. Foi incrível.


## 256 shades of R, G and B

**Slides**: [https://speakerdeck.com/almirfilho/256-shades-of-r-g-and-b](https://speakerdeck.com/almirfilho/256-shades-of-r-g-and-b)

A dupla [Almir Filho](https://twitter.com/almirfilho) e [Caio Gondim](https://twitter.com/caio_gondim) falaram sobre tudo que envolve cores. Praticamente uma aula de física misturada com artes, teoria das cores, acessibilidade e UX.

Interessante saber as "gambiarras" que são feitas para "enganar" nosso cérebro e fazê-lo enxergar tudo colorido nas telas, onde na verdade o que temos são apenas pequenos LEDs em vermelho, verde e azul.

Um ponto que sempre devemos levar em consideração é acessibilidade, e tivemos algumas dicas sobre isso. Evitar associar instruções de um sistema com cores específicas, exemplos como: "campos em vermelho são obrigatórios", ou "clique no ícone verde", etc, são más práticas e podem impedir que alguém com uma deficiência como daltonismo utilize seu site, ou aplicativo.


## Flexbox - o novo jeito de estruturar layouts

**Slides**: [http://www.slideshare.net/diegoeis/flexbox-to-the-people](http://www.slideshare.net/diegoeis/flexbox-to-the-people)

Para encerrar as palestras do evento, [Diego Eis](https://twitter.com/diegoeis) falou sobre o tão esperado flexbox, o novo módulo de CSS que traz várias melhorias na maneira como estruturamos layouts com CSS.

Primeiro ele deu um *background* sobre como temos estruturado layouts à décadas, e as várias gambiarras as quais temos recorrido com o passar dos anos, tais como tabelas, floats, inline-block e por aí vai.

Depois nos apresentou todas as novidades trazidas pelo flexbox, e rolou um *live coding* que deixou bem claro como será mais fácil e elegante criar layouts dessa nova maneira. Incrível.


## Episódio do ZOFE

Para encerrar, tivemos a honra de participar da gravação de um episódio do [ZOFE](http://zofe.com.br) ao vivo! Com direito ao famoso "Faaalaaa galeeeraaaa" do Daniel Filho e tudo mais. :-P

O assunto foi muito importante: **comunidade**.

Foram discutidas coisas como a participação das mulheres no mercado de TI e em eventos sobre desenvolvimento, a necessidade de termos novos membros da comunidade participando e dando palestras nos eventos, e a importância de reclamar menos e tomar a frente e fazer as coisas acontecerem, ou como disse o Caio Gondim: "Menos read, mais write".

Muito bom, e deixou muito o que se pensar.

Fique atento que em breve eles vão publicar esse episódio no site, aí você poderá entender melhor o assunto, e tirar suas conclusões.
