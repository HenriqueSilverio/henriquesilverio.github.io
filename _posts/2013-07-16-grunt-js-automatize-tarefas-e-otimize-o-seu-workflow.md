---
layout:     post
title:      Grunt JS - Automatize tarefas e otimize o seu workflow
date:       2013-09-03 15:00:00
summary:
categories: javascript-e-jquery
permalink:  /:categories/:title
---

<div style="text-align: center;">
    <img src="/images/grunt-javascript-task-runner.jpg" alt="Grunt JavaScript Task Runner">
</div>

Desenvolver um site ou aplicativo web moderno, é algo que está se tornando cada vez mais complexo. Por esse e outros motivos, todo bom desenvolvedor está sempre procurando novas maneiras de otimizar seu workflow visando tornar as coisas mais divertidas e aumentar sua produtividade sem perder a qualidade de seu trabalho.

Neste artigo irei apresentar o Grunt JS, uma excelente ferramenta criada por <a target="_blank" href="https://twitter.com/cowboy">Ben Alman</a>. Mostrarei  também um exemplo prático de uso, e espero que após lê-lo, você se sinta mais confortável com o Grunt JS e passe a adiciona-lo na “mistura” de seus próximos projetos.

## Grunt JS… o que é isso, afinal?

O Grunt JS é um poderoso task runner (automatizador de tarefas), que roda no terminal, e é gerenciado pelo <a target="_blank" href="https://npmjs.org/">NPM</a>, o gerenciador de pacotes para Node.js.
Legal, mas… por que eu devo aprender sobre Grunt JS?

Pelo “simples” fato da automatização de tarefas.

Já parou para pensar quanto tempo você perde toda vez que vai lançar um projeto em produção por exemplo? Você **concatena** e **minifica** (ou pelo menos deveria) seus arquivos de CSS e JavaScript, executa **testes unitários** e **linting** nos arquivos de JavaScript, **otimiza imagens** com ferramentas como [Smush.it](http://www.smushit.com/ysmush.it), [JPEGMini](http://www.jpegmini.com/), [TinyPNG](http://tinypng.org/) etc., **separa os arquivos gerados** e finalmente faz **deploy da aplicação**. E que dizer se você estiver usando um pré-processador de CSS como Sass? Mais uma tarefa na lista: **Compilar arquivos .scss ou .sass**.

Quanto menos tempo você perder executando tarefas repetitivas como essas citadas, mais fácil e produtivo se torna o seu trabalho. É aí que um task runner como o Grunt JS entra em ação. Uma vez configurado, o Grunt JS fará todo o “trabalho sujo” para você e/ou sua equipe, com praticamente nenhum esforço extra.

## Primeiros passos

Como você já deve ter percebido, para usar o Grunt JS é necessário ter o Node.js com o NPM instalados em sua máquina. Caso você ainda não tenha, o processo de instalação é muito simples. Acesse [nodejs.org](http://nodejs.org), clique no botão “Install” para fazer o download e execute o instalador. Feito isso você já terá o Node.js + NPM funcionando.

Agora abra seu console/terminal e vamos intalar o Grunt CLI (Grunt Command Line Interface). Se você trabalha em ambiente Windows, recomendo que utilize o [Windows PowerShell](http://microsoft.com/powershell/), rodando como administrador. Em Mac ou sistemas Unix, talvez você precise usar o sudo.

```
npm install -g grunt-cli
```

O comando acima irá instalar o Grunt CLI globalmente, e agora você pode usar o comando grunt em seu terminal. O Grunt CLI permite que você rode versões diferentes do Grunt em uma mesma máquina simultaneamente.

## Configurando um novo projeto com o Grunt

Todo projeto Grunt precisa de dois arquivos básicos: package.json e o Gruntfile.js. O package.json é um arquivo utilizado para guardar metadados de projetos que são publicados como módulos para o NPM, e o Gruntfile é um arquivo JavaScript ou CoffeeScript, utilizado para configurar tarefas e carregar os plugins do Grunt. Esses dois arquivos devem ser criados dentro da raiz de seu projeto, e devem sempre estar juntos no mesmo diretório.

## Aprendendo na prática

Para começar nosso exemplo prático, vamos criar um diretório chamado grunt-project e dentro dele iremos criar um subdiretório chamado src, que é onde iremos salvar o package.json e o Gruntfile.js. Nosso package.json terá um estrutura mais ou menos assim:

``` json
{
    "name": "project-name",
    "version": "0.1.0",
    "description": "Project description"
}
```

Você pode iniciar seguindo o modelo acima e edita-lo conforme suas necessidades. Para maiores informações sobre quais propriedades você pode usar, [consulte a documentação](https://npmjs.org/doc/json.html/). Você pode também dar uma olhada nesse [guia interativo](http://package.json.nodejitsu.com/), e conhecer diversas propriedades interessantes para acrescentar em sua configuração.

Com o package.json configurado, agora crie um novo arquivo de JavaScript e salve-o dentro do mesmo diretório src, ao lado de seu package.json, com o nome de Gruntfile.js.

O Gruntfile.js é composto por uma função que engloba todo o código, as configurações das tarefas do projeto, carregamento dos “grunt plugins” instalados (Veremos mais sobre como instalar plugins do grunt daqui a pouco) e o(s) registro(s) de sua(s) tarefas personalizadas.

Um Gruntfile.js básico pode ser feito seguindo essa estrutura:

``` javascript
"use strict";

module.exports = function( grunt ) {

    grunt.initConfig({

        // configurações das tarefas

    });

    // carregando plugins
    grunt.loadNpmTasks( 'plugin-name' );

    // registrando tarefas
    grunt.registerTask( 'default', [ 'watch' ] );

};
```

Dentro da função que engloba todo nosso código, temos alguns métodos sendo chamados, como: initConfig(), loadNpmTasks() e registerTask(). Vamos entendê-las melhor.

O método initConfig(), recebe um objeto JSON que será responsável por armazenar as configurações das tarefas de nosso projeto.

O loadNpmTaks() carrega um grunt plugin e permite que você use-o em seu Gruntfile. Você deve chamar esse método para todos os plugins que for utilizar. Carregar plugins vai se tornar algo muito chato conforme você for utiliando o Grunt com mais frequência, por isso mostrarei como você pode automatizar essa tarefa também.

E por fim o registerTask(), recebe dois argumentos: uma string e um array com o nome de uma ou mais tarefas que devem ser realizadas ao executar esse comando. Em nosso exemplo, ao rodar o comando grunt no terminal, ele irá chamar a tarefa default, executando as configurações definidas para o plugin watch.

## Instalando o Grunt e plugins úteis

Antes de fazermos nossas configurações, vamos instalar o Grunt e os plugins que iremos utilizar. Para instalar o Grunt, e marcá-lo como uma das dependências de seu projeto é simples:

```
npm install grunt --save-dev
```

Após rodar esse comando, você verá que um diretório node_modules foi criado, e visto que usamos `––save-dev`, também foi adicionada uma propriedade devDependencies dentro do package.json. Isso é muito importante, pois assim, caso esteja trabalhando com controle de versões, você não precisará incluir o diretório `node_modules` em seus commits, basta rodar o comando `npm install` e todas as dependências do projeto serão instaladas.

O processo de instalação de plugins é o mesmo. Geralmente existe um plugin específico para qualquer tarefa que você queira realizar. Literalmente são milhares de plugins que já foram criados para o Grunt. Você pode consultar essa lista extensa de plugins.

Vamos agora instalar os plugins que iremos utilizar:

```
npm install matchdep --save-dev
npm install grunt-contrib-watch --save-dev
npm install grunt-contrib-compass --save-dev
npm install grunt-contrib-uglify --save-dev
npm install grunt-ftp-deploy --save-dev
```

Com o Grunt e os plugins que precisaremos instalados, agora vamos configurar nossas tasks e finalmente ver a “mágica” funcionando. Explicarei as configurações uma a uma dos plugins instalados acima, e no final você poderá consultar o código fonte completo.

## Carregando todas as taks do Grunt automaticamente

O primeiro plugin que iremos configurar é o [matchdep](https://npmjs.org/package/matchdep/).

Conforme comentei anteriormente, cada vez que você for usar um novo plugin, será necessário adicionar uma chamada ao método loadNpmTasks(). Isso traz um trabalho chato e demanda manutenção desnecessária sempre que for adicionar ou remover um plugin.

Felizmente com o plugin matchdep nós cortamos esse problema pela raiz. O que esse plugin faz é o seguinte: Ele extrai informações gravadas em seu package.json, e chama o método loadNpmTasks() para cada plugin instalado.

``` javascript
require("matchdep").filterDev("grunt-*").forEach(grunt.loadNpmTasks);
```

Pronto. Você nunca mais precisará adicionar ou remover chamadas ao método loadNpmTasks() manualmente de novo.

## Executando tarefas após alterar arquivos

Com o plugin grunt-contribu-watch, criamos uma task chamada “watch”. Ao rodar essa tarefa, o Grunt irá “observar” os arquivos do nosso projeto, e quando fizermos qualquer alteração em um dos arquivos especificados, ele irá executar outras tarefas que foram atreladas a ela automaticamente. Isso é fantástico, pois dessa forma você pode executar várias tarefas automaticamente com apenas um único comando.

``` javascript
// Watch
watch: {
    css: {
        files: [ '../assets/scss/**/*' ],
        tasks: [ 'compass' ]
    },
    js: {
        files: '../assets/js/**/*',
        tasks: [ 'uglify' ]
    }
},
```

Nesse exemplo, sempre que algum arquivo dentro do diretório ‘assets/scss’ for alterado, o Grunt irá executar a tarefa ‘compass’ para compilar o código Sass. E sempre que editarmos um arquivo dentro do diretório ‘assets/js’ o Grunt irá executar a tarefa ‘uglify’ para concatenar e minificar os arquivos JavaScript.

Veremos como configurar essas tarefas logo abaixo.

## Compilar Sass usando Compass

Se você trabalha com Sass + Compass, compilar seu código para CSS é muito simples usando o plugin [grunt-contrib-compass](https://github.com/gruntjs/grunt-contrib-compass). Em nosso exemplo, definimos a propriedade force como true, para permitir que o Compass sobrescreva arquivos, indicamos o caminho para um arquivo config.rb que contém as demais configurações do Sass e determinamos que o código compilado sairá minificado.

Se você não está familiarizado com o arquivo config.rb que foi citado, [leia a documentação](http://compass-style.org/help/tutorials/configuration-reference/) para obter maiores informações. Então criamos nosso arquivo config.rb e adicionamos o seguinte código em nosso Gruntfile.js:

``` javascript
// Compile scss
compass: {
    dist: {
        options: {
            force: true,
            config: 'config.rb',
            outputStyle: 'compressed'
        }
    }
},
```

## Concatenando e minificando JavaScript

Para concatenar e minificar nossos arquivos de JavaScript, vamos utilizar o plugin grunt-contrib-uglify. As configurações dessa task também são muito simples. Na propriedade files, passamos um objeto com local onde o arquivo minificado será gravado, que recebe um array de arquivos a serem concatenados e minificados:

``` javascript
// Concat and minify javascripts
uglify: {
    options: {
        mangle: false
    },
    dist: {
        files: {
            '../build/js/app.min.js': [
                '../assets/js/app.js'
            ]
        }
    }
},
```

## Fazendo deploy do projeto

Conforme comentei no inicio do artigo, o Grunt também pode ajudar você na hora de fazer deploy de seus projetos em um servidor. Se o seu host lhe dá acesso via SSH, você pode utilizar o plugin [grunt-rsync](https://github.com/jedrichards/grunt-rsync) para isso.

Mas em alguns casos você terá acesso apenas via FTP. Não se preocupe, para isso iremos utilizar o plugin [grunt-ftp-deploy](https://github.com/zonak/grunt-ftp-deploy).

Para que o grunt-ftp-deploy funcione, vamos precisar adicionar um arquivo chamado .ftppass dentro do diretório src do nosso projeto, junto com Gruntfile.js, package.json e o config.rb. Este arquivo é um objeto JSON que armazena os dados de login do seu FTP. Tome cuidado com esse arquivo quando estiver usando Git ou outro sistema de versionamento de arquivos. O .ftppass segue essa estrutura:

```
{
    "key1": {
        "username": "your-ftp-user",
        "password": "your-ftp-pass"
    }
}
```

Agora que já temos nosso nome de usuário e senha guardados no arquivo .ftppass, vamos voltar ao nosso Gruntfile.js e configurar a task para fazer o deploy em nosso servidor.

Basta trocar o valor da propriedade ‘host’ para o host do seu site e o valor de ‘dest’ para o caminho onde você irá upar seus arquivos. Em ‘exclusions’ você pode especificar que arquivos e diretórios não devem ser enviados para o servidor junto com sua aplicação.

``` javascript
// FTP deployment
'ftp-deploy': {
    build: {
        auth: {
            host: 'ftp.yoursite.com',
            port: 21,
            authKey: 'key1'
        },
        src: '../',
        dest: '/www/my-app/',
        exclusions: [
            '../**/.DS_Store',
            '../**/Thumbs.db',
            '../.git',
            '../.gitignore',
            '../README.md',
            '../src',
            '../assets'
        ]
    }
}
```

## Juntando tudo e testando

Se você está acompanhando o artigo com atenção, nesse ponto você já terá todas as tarefas do Grunt configuradas. Vamos adicionar as duas últimas linhas de código em nosso Gruntfile.js para registrar duas tarefas personalizadas: watch e deploy.

``` javascript
// registrando tarefa default
grunt.registerTask( 'default', [ 'watch' ] );

// registrando tarefa para deploy
grunt.registerTask( 'deploy', [ 'ftp-deploy' ] );
```

Registrando essas tarefas, agora quando usarmos o comando “grunt” no terminal, será executada a task “watch” conforme já foi explicado anteriormente, e quando usarmos o comando “deploy”, irá rodar nossa task que fará deploy para o servidor.

Então a versão final do nosso Gruntfile.js ficou assim:

``` javascript
"use strict";

module.exports = function( grunt ) {

    // Load all tasks
    require("matchdep").filterDev("grunt-*").forEach(grunt.loadNpmTasks);

    grunt.initConfig({

        // Watch
        watch: {
            css: {
                files: [ '../assets/scss/**/*' ],
                tasks: [ 'compass' ]
            },
            js: {
                files: '../assets/js/**/*',
                tasks: [ 'uglify' ]
            }
        },

        // Compile scss
        compass: {
            dist: {
                options: {
                    force: true,
                    config: 'config.rb',
                    outputStyle: 'compressed'
                }
            }
        },

        // Concat and minify javascripts
        uglify: {
            options: {
                mangle: false
            },
            dist: {
                files: {
                    '../build/js/app.min.js': [
                        '../assets/js/app.js'
                    ]
                }
            }
        },

        // FTP deployment
        'ftp-deploy': {
            build: {
                auth: {
                    host: 'ftp.yoursite.com',
                    port: 21,
                    authKey: 'key1'
                },
                src: '../',
                dest: '/www/my-app/',
                exclusions: [
                    '../**/.DS_Store',
                    '../**/Thumbs.db',
                    '../.git',
                    '../.gitignore',
                    '../README.md',
                    '../src',
                    '../assets'
                ]
            }
        }

    });

    // registrando tarefa default
    grunt.registerTask( 'default', [ 'watch' ] );

    // registrando tarefa para deploy
    grunt.registerTask( 'deploy', [ 'ftp-deploy' ] );

};
```

Em seu terminal acesse o diretório src e rode o comando:

```
grunt
```

Altere um arquivo do diretório assets/scss e assets/js e você verá que será gerado o diretório build com os arquivos minificados prontos para deploy.

Volte ao terminal e pressione CTRL + C para encerrar a task watch.

Agora para fazer o deploy, rode o comando abaixo e aguarde os arquivos serem enviados para seu servidor conforme especificado em suas configurações:

```
grunt deploy
```

Muito bem! Se você acompanhou tudo com atenção, com apenas um único comando você compilou arquivos scss, concatenou e minificou arquivos de JavaScript e gerou uma build do seu projeto. E com apenas mais um simples comando, você fez o deploy dessa build.

Eu disse… parece mágica não é mesmo? =D

### Conclusão

Ferramentas como o Grunt JS só nos trazem grandes beneficios e estão aí disponíveis para quem quiser usar. Além das opções ensinadas nesse artigo, existem muitas outras coisas que o Grunt pode fazer, e você deve pesquisar sobre elas.

Espero que você tenha se interessado e pesquise mais para adaptar o Grunt as suas necessidades. Sem dúvida você não irá se arrepender se tirar um tempo para estudar e integrar esse tipo de ferramenta em seu workflow.

O código fonte do projeto desenvolvido nesse artigo está disponível no Github. Você pode clonar o repositório e personaliza-lo para seus projetos. Sinta-se a vontade para enviar sugestões e tirar suas dúvidas nos comentários.

Outros links sobre Grunt:

* [Official documentation](http://gruntjs.com/getting-started)
* [Introducing Grunt](http://weblog.bocoup.com/introducing-grunt/)
* [Get Up And Running With Grunt.js](http://moduscreate.com/get-up-and-running-with-grunt-js/)
* [Advanced Grunt tooling](http://chrisawren.com/posts/Advanced-Grunt-tooling)
* [Building JavaScript projects with Grunt](http://ruudud.github.io/2012/12/22/grunt/)
* [Grunt.js Parte 1 – Instalando Node.js](http://www.newaeonweb.com.br/n3/grunt-js-parte-1-instalando-node-js.html)
* [GruntJS – Por onde começar?](http://www.voltsdigital.com.br/labs/gruntjs-por-onde-comecar/)
* [Automação de build de front-end com Grunt.js](http://blog.caelum.com.br/automacao-de-build-de-front-end-com-grunt-js/)
