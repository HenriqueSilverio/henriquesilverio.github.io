---
layout:     post
title:      Review do livro "Maintainable JavaScript"
date:       2014-05-11 23:30:00
summary:
categories: javascript-e-jquery
permalink:  /:categories/:title
---

Semana passada (mais especificamente dia 04/05/2014) terminei a leitura do livro "<strong>Maintainable JavaScript</strong>" escrito por <strong>Nicholas C. Zakas</strong>. Resolvi então fazer um review com algumas considerações que achei importante em cada capítulo.

O texto ficou um pouco grande (como de costume em meus posts), então se você estiver apenas querendo uma opinião direta sobre o livro, se vale ou não comprar e ler, a minha resposta é: <b>sim, vale a pena</b>.

O que tenho à dizer é que foi uma leitura de "duzentas e poucas" páginas muito interessante. Em apenas um final de semana você pode obter bastante conteúdo de qualidade lendo esse livro.

Sem mais, vamos ao review!

<img src="/images/Maintainable-JavaScript.jpg" alt="Maintainable-JavaScript">

<h2>Introduction</h2>

Em uma breve introdução, o autor comenta sobre a dificuldade que temos tido ultimamente no ambiente profissional na área de desenvolvimento Web, visto que pessoas que fazem parte de uma equipe grande possuem diferentes backgrounds e formas de resolver problemas no dia a dia.

A importância de se escrever código manutenível fica ainda mais evidente quando nos damos conta de que na realidade, ao invés de sempre criar coisas novas, do zero, gastamos a maior parte de nosso tempo dando manutenção em código já existente.

Acho interessante abrir aqui uma observação, que segundo Roger Pressman, em seu livro sobre Engenharia de Software, 60% do esforço de uma fábrica de software é dedicado à manutenção de sistemas já existentes. Pense por um instante quanto tempo e dinheiro envolve isso!

Com isso em mente, é importante escrever código não como se ele fosse exclusivo para você, mas sim pensando nos desenvolvedores que vão trabalhar com ele depois de você. E fazer parte de uma equipe, não significa tomar decisões que são melhores no seu ponto de vista, mas sim as que são melhores para a sua equipe como um todo.


<h2>Part 1: Style Guidelines</h2>

Esta parte do livro é focada em padrões de escrita de código, envolve a parte "visual", a "formatação/aparência" do código. Embora seja um tópico ignorado por muitos, esse é um ponto super importante quando se trabalha em equipe ou ao colaborar em projetos open source. Seguindo padrões no que diz respeito à maneira como se escrever código, faz parecer que o software foi escrito por um único desenvolvedor, mesmo que ele tenha passado pela mão de vários membros da equipe ao longo do projeto, o que elimina problemas de inconsistência e evita desperdicío de tempo. Nesta seção, o autor apresenta também as ferramentas <a href="http://www.jslint.com/" target="_blank">JSLint</a> e <a href="http://www.jshint.com/" target="_blank">JSHint</a>, que são indispensáveis hoje em dia.

<h3>Chapter 1: Basic Formatting</h3>

Aqui começa-se a definir um guia de estilos, com os padrões que deverão ser seguidos a risca por toda a equipe. Cada tópico apresentado é seguido de um "porque" e exemplos, facilitando bem o entendimento. Entre os assuntos abordados estão: níveis de identação (tab ou espaços?), terminação de instruções (com ou sem ponto-e-vírgula?), tamanho de linha, quebras de linha, nomenclatura de variáveis e funções, uso de valores literais para Strings, Números, Arrays, Objetos, etc.

<h3>Chapter 2: Comments</h3>

Este capítulo trata sobre padrões ao escrever comentários. Dicas sobre quando comentar o código e de forma correta, utilizando comentários inline ou de multiplas linhas nas ocasiões certas. O capítulo termina com uma passada rápida sobre o uso de comentários para gerar documentação.

<h3>Chapter 3: Statements and Expressions</h3>

Formatação de estruturas condicionais <code>if</code>, <code>else</code>, laços de repetição e iteração, bem como instrução <code>swtich</code> são os assuntos abordados nesse capítulo. Espaçamentos, alinhamentos, etc., tudo para deixar o código mais legível.

<h3>Chapter 4: Variables, Functions, and Operators</h3>

Falando sobre variáveis, aqui Zakas nos alerta sobre um comportamento muitas vezes mal entendido, e que prega peças em alguns desenvolvedores: <b>hoisting</b>. Logo após, o assunto são as funções: declaração, invocação e <a href="http://benalman.com/news/2010/11/immediately-invoked-function-expression/" target="_blank">Immediately-Invoked Function Expression</a> (IIFE, tão famosas "funções imediatas"). Em seguida, temos algumas dicas sobre o <a href="http://loopinfinito.com.br/2013/07/16/javascript-strict-mode/" target="_blank">modo estrito</a> e como podemos nos beneficiar por usar esse cara. Por fim, somos alertados sobre o uso de <code>eval()</code> e comparações de igualdade que podem gerar resultados um tanto quanto estranhos.

<h2>Part 2: Programming Practices</h2>

Nessa segunda seção do livro, são abordados alguns padrões de projetos e dicas de programação. Práticas que resolvem problemas já conhecidos pela comunidade e que podem/devem ser aplicados em nossos projetos também.

<h3>Chapter 5: Loose Coupling of UI Layers</h3>

Promover o fraco acoplamento é uma boa prática já bem difundida em engenharia de software, e em aplicações JavaScript não é diferente. A própria natureza de aplicativos Web promove essa ideia. HTML, CSS, JavaScript: três camadas com diferentes papéis que juntas entregam uma experiência completa para o usuário, mas que uma não devem invadir o território uma das outras por assim dizer. Neste capítulo temos algumas dicas interessantes, incluindo sobre templates no client-side (ex: <a href="http://handlebarsjs.com/" target="_blank">Handlebars</a>) e uma temos relatada uma experiência que o próprio Zakas passou ao trabalhar na equipe do Yahoo! em 2005.

<h3>Chapter 6: Avoid Globals</h3>

No ambiente JavaScript dos browsers, o objeto <code>window</code> atua como uma espécie de objeto global, e qualquer variável ou função declarada em escopo global se torna uma propriedade desse objeto. Por isso, quanto mais variáveis globais você declarar, maiores são as chances de introduzir erros em sua aplicação. Este capítulo apresenta quais são esses erros e também dicas de como evitá-los. Para isso, são explicadas algumas abordagens como "uma única variável global", "namespaces" e "módulos" (ex: AMD, <a href="http://requirejs.org/" target="_blank">RequireJS</a>).

<h3>Chapter 7: Event Handling</h3>

Uma das características mais importantes do JavaScript é o poder que temos para manipular eventos. Mas essa também é uma área problemática quando se trata de compatibilidade entre os diversos browsers e ambientes em que uma aplicação poderá rodar, por isso exige bastante atenção. De forma breve, mas bem explicada, este capítulo mostra algumas abordagens para manter a manutenibilidade ao lidar com eventos.


<h3>Chapter 8: Avoid Null Comparisons</h3>

Este capítulo mostra algumas armadilhas de se utilizar o operador <code>typeof</code> e como checar valores de forma correta ao comparar valores em validações, tais como o uso do operador <code>instanceof</code> e técnicas para identificar <code>Array</code>s com a função nativa <code>Array.isArray()</code> introduzida em ECMAScript 5 e um polyfill para uso cross-browser, e por fim o uso do método <code>hasOwnProperty</code> para identificar propriedades em objetos.

<h3>Chapter 9: Separate Configuration Data from Code</h3>

Uma forma de aumentar a flexibilidade em uma aplicação, é fazer o uso de dados de configuração ao invés de inserir esses dados diretamente no código. Este capítulo vai lhe ajudar a identificar o que são esses "dados de configuração" e como utilizá-los.

<h3>Chapter 10: Throw Your Own Errors</h3>

Como Zakas diz logo no inicio desse capítulo: "lançar erros é uma arte" e nós como programadores, não devemos ter medo de erros, muito pelo contrário, eles nos ajudam. Em JavaScript temos recursos como o operador <code>throw</code> e instruções <code>try-catch</code> para lançar erros personalizados, além de alguns tipos de erros nativos do browser. Nesse capítulo o autor nos apresenta esses caras, e dá dicas sobre como identificar a hora certa de lançar erros, para que eles facilitem nosso dia a dia.

<h3>Chapter 11: Don’t Modify Objects You Don’t Own</h3>

Em JavaScript podemos alterar praticamente qualquer objeto que encontrarmos pela frente. Essa é uma das muitas características que tornam JavaScript uma linguagem muito flexível. Mas esse poder também traz alguns perigos, e esse capítulo explica quais são eles, e também como evitá-los. Temos uma visão geral sobre herança, protótipos e um <strong>design pattern</strong> conhecido como <b>facade</b>. Por fim também são mostrados alguns métodos de ECMAScript 5 que podem ser utilizados para prevenir que objetos sejam alterados indevidamente.

<h3>Chapter 12: Browser Detection</h3>

Nos primórdios da Web era muito comum fazer uma espécie de "farejamento de browser" para identificar qual navegador o usuário estaria utilizando e servir código específico para ele. Conforme esse capítulo mostra, essa abordagem traz sérios problemas de manutenibilidade e deve ser evitada ao máximo. Aqui também são mostradas quais alternativas podemos utilizar para lidar com essas diferenças entre navegadores sem prejudicar a manutenibilidade do código.

<h2>Part 3: Automation</h2>

Automação é um ponto chave para desenvolvedores JavaScript modernos. Aplicações de hoje em dia, não raramente possuem milhares de linhas de código JavaScript e são mantidas talvez por dezenas de desenvolvedores diferentes, por isso precisamos de ferramentas para facilitar nossa vida, automatizando processos repetitivos. Essa seção do livro mostra como podemos tirar vantagem de ferramentas de automação no desenvolvimento JavaScript.

Essa pode não ter sido minha seção preferida do livro, pois abrange ferramentas baseadas em Java, e hoje em dia temos as mesmas funcionalidades (diria que até melhores) em ferramentas feitas apenas com JavaScript como <a href="http://blog.henriquesilverio.com/javascript-e-jquery/grunt-js-automatize-tarefas-e-otimize-o-seu-workflow/" target="_blank">Grunt</a>, <a href="http://gulpjs.com/" target="_blank">Gulp</a> entre várias outras. Mas vale a leitura pois os conceitos apresentados podem ser adaptados a qualquer ferramenta de automação que você escolha utilizar.

<h3>Chapter 13: File and Directory Structure</h3>

Antes de integrar um sistema de automação em sua aplicação, é importante planejar e organizar as coisas. Como você organiza o código do seu projeto? Já chega de <a href="http://en.wikipedia.org/wiki/Spaghetti_code" target="_blank">código espaguete</a> né? Esse capítulo faz uma análise da estrutura de diretórios e arquivos de alguns projetos grandes como a biblioteca <a href="http://jquery.com/" target="_blank">jQuery</a>, <a href="http://dojotoolkit.org/" target="_blank">Dojo</a> e <a href="http://yuilibrary.com/" target="_blank">YUI</a>, onde podemos tirar algumas lições.

<h3>Chapter 14: Ant</h3>

Após pensar um pouco e estruturar as coisas, agora o capítulo 14 apresenta e mostra como fazer as configurações iniciais no <a href="http://ant.apache.org" target="_blank">Ant</a>, uma ferramenta originalmente construída para build de projetos Java e com sintaxe XML para configurar suas tasks.

<h3>Chapters 15, 16 and 17</h3>

Esses capítulos avançam na configuração de tasks do Ant, tais como: validações, concatenação, minificação e compressão arquivos. Sem mais, recomendo fortemente que ao invés disso, utilize o <a href="http://gruntjs.com/" target="_blank">Grunt</a> para esse tipo de coisa.

<h3>Chapter 18: Documentation</h3>

Todo mundo prefere escrever código do que documentações. Por sorte, também temos ferramentas que nos ajudam com isso. Esse capítulo apresenta ferramentas que podem ser utilizadas para gerar automaticamente documentações para aplicações JavaScript com base em comentários feitos no código. Muito bom, vale a pena conferir e por em prática.

<h3>Chapter 19: Automated Testing</h3>

Testar código pode ser algo muito doloroso. Testar JavaScript pode ser ainda pior. Já pensou na quantidade de browsers, sistemas operacionais e dispositivos diferentes em que sua aplicação vai ser executada? Agora imagine só ter que testá-la em todas essas variações de forma manual... impossível! Com as dicas desse capítulo, podemos obter uma visão geral de ferramentas para testes automatizados, uma que acho muito interessante é o <a href="http://phantomjs.org/" target="_blank">PhantomJS</a>.

<h3>Chapter 20: Putting It Together</h3>

Para fechar a última seção do livro, este capítulo fala sobre planejar um workflow de build, com diversos ambientes e um sistema de CI (Continuous Integration), no caso foi apresentado o <a href="http://jenkins-ci.org/" target="_blank">Jenkins</a>. As vantagens desse tipo de ferramenta são enormes.

<h3>Appendix A: JavaScript Style Guide</h3>

Após todas as considerações feitas, temos um "Guia de Estilos" com as preferências de estilo de programação do Nicholas Zakas para todos os tópicos abordados em seu livro. Uma boa ideia seria utilizar isso como modelo e documentar suas preferências e passar a adotar um padrão em sua equipe, caso ainda não o façam.

<h3>Appendix B: JavaScript Tools</h3>

Uma lista de ferramentas para desenvolvedores JavaScript, com links para onde pode encontrá-las. Desde ferramentas de build, geradores de documentação e linting até testes automatizados.

<h2>Conclusão</h2>

Se você procura escrever JavaScript de forma profissional, acabar com problemas de inconsistência e desperdício de tempo para resolver problemas "bobos" ao trabalhar em equipes grandes ou colaborar em projetos open source, esse livro vai te ajudar muito.
