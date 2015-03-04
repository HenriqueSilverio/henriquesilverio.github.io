---
layout:     post
title:      Como utilizar API de Geolocalização HTML5
date:       2013-09-03 15:00:00
summary:
categories: javascript-e-jquery
---

Nesse artigo irei mostrar **como utilizar geolocalização com HTML5**. O uso dessa API é muito simples, e as possibilidades de aplicações que ela nos traz são fantásticas, sendo assim um recurso muito bacana para sites e aplicações web modernas.

<div style="text-align: center;">
    <img src="/images/html5-geolocation-api.png" alt="HTML5 Geolocation API">
</div>

## Geolo... quê?

Entre as diversas novas API's que chegaram com o HTML5, está a <a href="http://www.w3.org/TR/geolocation-API/" target="_blank">Geolocation API</a>. O que essa API faz? Simples. Com ela nós podemos descobrir onde o usuário está localizado de maneira bem precisa, e capturar alguns dados como suas coordenadas de latitude e longitude.

Com esses dados em "mãos" por exemplo, você pode usar a <a href="https://developers.google.com/maps/documentation/javascript/" target="_blank">Google Maps API</a> para exibir um mapa mostrando onde o usuário está, traçar uma rota para ajudá-lo a chegar em determinado local, exibir locais úteis como restaurantes, lojas, etc. que estão por perto do usuário e podem interessá-lo, enfim, o limite será sua criatividade. O legal é explorar as possibilidades e não ficar apenas no "<a href="http://tableless.com.br/creme-de-papaia-e-geolocalizacao/" target="_blank">creme de papaia de sempre</a>".

## Que browsers suportam a API de Geolocalização?

O suporte à API de Geolocalização é bem amplo, funciona na grande maioria dos browsers, com exceção apenas o IE<del>ca</del>8- e o Opera Mini 5.0 - 7.0. Você pode conferir esses dados no site <a href="http://caniuse.com/#search=geolocation" target="_blank">Can I Use</a>.

Para verificar se o browser suporta a API de geolocalização HTML5, podemos utilizar a biblioteca <a href="http://modernizr.com" target="_blank">Modernizr</a> ou fazer uma checagem simples com JavaScript "puro":

``` javascript
if( ! 'geolocation' in navigator ) {
    // Não suporta Geolocation HTML5...
} else {
    // Suporta Geolocation HTML5. Vamos em frente!
}
```
## Mergulhando mais a fundo

Agora vamos realmente entender como as coisas funcionam nessa API. Se você abrir o console <a href="http://getfirebug.com/" target="_blank">Firebug</a> ou outra ferramenta de inspeção em seu browser favorito, verá que o objeto geolocation é composto por três métodos, que são: `clearWatch()`, `getCurrentPosition()` e `watchPosition()`. Veremos como trabalhar com cada um desses métodos.

<div style="text-align: center;">
    <img src="/images/HTML5-Geolocation-Firebug.jpg" alt="Objeto Geolocation no Firebug">
</div>

## O método getCurrentPosition()

Para fins didáticos, vamos começar analisando o método `getCurrentPosition()`. Esse método pode receber três argumentos que são:


* **successCallback**: Uma função que será executada caso a posição do usuário seja localizada com sucesso;
* **errorCallback**: Uma função que será utilizada para tratar eventuais erros ao se tentar obter a localização do usuário. Esse parâmetro é opcional;
* **PositionOptions**: Um objeto com propriedades de configurações adicionais. Esse parâmetro também é opcional.

`getCurrentPosition()` é chamado da seguinte forma:

```javascript
navigator.geolocation.getCurrentPosition( geoSuccess );
```

Quando esse método é chamado, ele exibe uma notificação solicitando permissão do usuário para detectar sua posição, e caso o usuário concorde (não, você não pode acessar a localização do usuário sem que ele permita), ele executa uma requisição assíncrona para detectar sua posição atual e chama um callback para tratar os dados retornados. Por isso você sempre deve especificar o primeiro argumento de `getCurrentPosition()`.

A função callback de sucesso, recebe um único argumento e retorna um objeto com duas propriedades: **coords** e **timestamp**. A propriedade timestamp serve apenas para armazenar a data e o horário de quando a localização foi calculada. E a propriedade coords é um objeto com propriedades interessantes como latitude e longitude.

Após implementar a função callback `geoSuccess()` nosso código ficou assim:

```javascript
function geoSuccess( pos ) {
    // armazena as coordenadas de latitude e longitude
    var lat = pos.coords.latitude,
        lng = pos.coords.longitude;

    // crie qualquer coisa legal usando as coordenadas
};

navigator.geolocation.getCurrentPosition( geoSuccess );
```

## Tratando erros

Durante o ciclo de uso da geolocalização alguns erros podem ocorrer, e a API nos fornece recursos para tratar esses possíveis erros de maneira bem simples. Para isso, basta usar o segundo parâmetro que é uma função callback para tratar erros, conforme já citado anteriormente. Cada erro retornado é referenciado por um código. Os erros que podem ser retornados e seus respectivos códigos são:


* **1 - PERMISSION_DENIED:** O usuário não aceitou compartilhar sua posição. O ideal nesse caso é não incomodar o usuário com mensagens de erro.
* **2 - POSITION_UNAVAILABLE:** O usuário está desconectado, não foi possível alcancar os satélites de GPS ou algo do tipo.
* **3 - TIMEOUT:** A requisição demorou demais para retornar a posição do usuário. Você pode determinar qual é o tempo limite máximo, veremos como fazer isso.
* **0 - UNKNOWN_ERROR:** Ocorreu um erro desconhecido.

```javascript
function geoSuccess( pos ) {
    // armazena as coordenadas de latitude e longitude
    var lat = pos.coords.latitude,
        lng = pos.coords.longitude;

    // crie qualquer coisa legal usando as coordenadas
}

function geoError( err ) {
    switch( err.code ) {
        case 1:
            // permissão negada pelo usuario
            break;

        case 2:
            // nao foi possível alcançar os satélites GPS
            break;

        case 3:
            // a requisição demorou demais para retornar
            break;

        case 0:
            // ocorreu um erro desconhecido...
            break;
    }
}

navigator.geolocation.getCurrentPosition( geoSuccess, geoError );
```
## Configurações adicionais

Agora que já temos uma função para capturar a posição do usuário e outra para tratar os possíveis erros, podemos também opicionalmente utilizar um terceiro parâmetro, que é o objeto **PositionOptions**. Esse objeto possui três proriedades que são:

* **enableHighAccuracy**: Um valor boolean, por padrão false. Se definir como true, e o dispositivo do usuário suportar tal funcionalidade, irá tentar utilizar GPS para aumentar a precisão da localização, por exemplo.
* **timeout**: Aqui definimos o tempo máximo em milisegundos que a requisição poderá demorar antes de disparar um erro TIMEOUT que vimos acima.
* **maximumAge**: O tempo máximo em milisegundos que o dispositivo pode fazer um cache da localização do usuário.

```javascript
function geoSuccess( pos ) {
    // armazena as coordenadas de latitude e longitude
    var lat = pos.coords.latitude,
        lng = pos.coords.longitude;

    // crie qualquer coisa legal usando as coordenadas
}

function geoError( err ) {
    switch( err.code ) {
        case 1:
            // permissão negada pelo usuario
            break;

        case 2:
            // nao foi possível alcançar os satélites GPS
            break;

        case 3:
            // a requisição demorou demais para retornar
            break;

        case 0:
            // ocorreu um erro desconhecido...
            break;
    }
}

var geoOptions = {
    enableHighAccuracy: true,
    timeout: 30000,
    maximumAge: 3000
};

navigator.geolocation.getCurrentPosition( geoSuccess, geoError, geoOptions );
```

## watchPosition() e clearWatch()

Ao invés de apenas pegar a localização do usuário, nós podemos também acompanhar continuamente sua posição, atualizando as coordenadas sempre que o usuário se mover. Para isso nós utilizamos o método **watchPosition()**. Esse método funciona da mesma forma que o **getCurrentPosition()**, a única diferença é que a função **geoSuccess()** do nosso exemplo será chamada toda vez que o usuário se locomover, e o método **watchPosition()** retorna um número, para que possamos parar de rastrear a posição do usuário quando desejarmos.

Para parar de rastrear a posição do usuário, basta utilizarmos o método **clearWatch()** passando à ele como argumento o número retornado pelo método **watchPosition()**. Veja agora um exemplo:

```javascript
// callback para tratar posição do usuário
function geoSuccess( pos ) {
    // armazena as coordenadas de latitude e longitude
    var lat = pos.coords.latitude,
        lng = pos.coords.longitude;

    // crie qualquer coisa legal usando as coordenadas
}

// callback para tratar erros
function geoError( err ) {
    switch( err.code ) {
        case 1:
            // permissão negada pelo usuario
            break;

        case 2:
            // nao foi possível alcançar os satélites GPS
            break;

        case 3:
            // a requisição demorou demais para retornar
            break;

        case 0:
            // ocorreu um erro desconhecido...
            break;
    }
}

var geoOptions = {
    enableHighAccuracy: true,
    timeout: 30000,
    maximumAge: 3000
};

// um botão "stop"
var btnStop = document.getElementById( 'btn-stop' );

// rastreia posicao do usuario continuamente
var watch = navigator.geolocation.watchPosition( geoSuccess, geoError, geoOptions );

// para de rastrear posiçãoo do usuário ao clicar no botão "stop"
btnStop.addEventListener( "click", function() {
    navigator.geolocation.clearWatch( watch );
}, false );
```

## Finalizando

Neste artigo você conheceu a API de Geolocalização HTML5 e viu alguns exemplos de código para se trabalhar com ela. Essa API sem dúvida será de grande ajuda para tornar suas aplicações mais ricas e interativas. Conforme já mencionado no artigo, você pode integrar o uso dessa API com outros serviços, API's sociais etc., para criar coisas muito legais.

Você já usou a API de Geolocalização HTML5 em algum projeto? Gostou do artigo e pretende fazer algum experimento? Não gostou do artigo ou tem dúvidas? Fique a vontade para compartilhar suas experiências nos comentários.

### Referências:

* <a href="http://www.w3c.br/cursos/html5/conteudo/capitulo24.html" target="_blank">Apostila W3C - Geolocation API</a>
* <a href="https://developer.mozilla.org/en-US/docs/WebAPI/Using_geolocation" target="_blank">Using geolocation - Mozilla Developer Network</a>
* <a href="http://diveintohtml5.com.br/geolocation.html" target="_blank">Dive into HTML5</a>
