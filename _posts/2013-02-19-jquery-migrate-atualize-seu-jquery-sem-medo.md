---
layout:     post
title:      jQuery Migrate – Atualize seu jQuery sem medo
date:       2013-02-19 19:30:00
summary:    Para evitar erros é importante ficar atento ao atualizar o jQuery em um projeto que está rodando em produção. Para nos ajudar nesse upgrade, agora temos o plugin jQuery Migrate.
categories: javascript-e-jquery
permalink:  /:categories/:title
---

![jQuery Migrate](/images/jquery-migrate.jpg)

No dia 4 de Fevereiro desse ano, a equipe do **jQuery** anunciou oficialmente a versão 1.9.1 da **biblioteca JavaScript** mais utilizada no mundo.

Desde o lançamento da versão 1.9 vários bugs das versões anteriores tem sido corrigidos e uma porção de novos recursos estão sendo implementados, como por exemplo o suporte cross-browser à alguns **seletores CSS3** para manipular elementos no **DOM**.

Como o objetivo desse artigo não é focar nas novidades do **jQuery 1.9**, você pode acessar o upgrade guide no site oficial do **jQuery** para maiores informações sobre isso.

## Resolvendo problemas de maneira simples

Naturalmente, assim como alguns novos recursos estão sendo adicionados à biblioteca, outros também estão ficando obsoletos e foram removidos. Para evitar erros é importante ficar atento ao atualizar o **jQuery** em um projeto que está rodando em produção.

Para nos ajudar nesse upgrade de projetos que utilizam uma versão antiga do jQuery, a equipe de desenvolvedores da biblioteca criou um plugin chamado [jQuery Migrate](http://blog.jquery.com/2013/02/16/jquery-migrate-1-1-1-released).

O plugin **jQuery Migrate** é utilizado para detectar e restaurar APIs e/ou features obsoletas do **jQuery** que foram removidas com o lançamento da versão 1.9. Você também pode utilizar a versão uncompressed do **jQuery Migrate** para diagnosticar problemas de incompatibilidade gerando mensagens de alertas que irão lhe auxiliar a encontrar esses problemas e resolve-los.

Esse plugin pode ser utilizado em conjunto com o **jQuery 1.9.x** ou com o **2.0 Beta**. Atualizar sua versão do **jQuery** e utilizar o **jQuery Migrate** é muito fácil, basta inserir o snippet abaixo em seu código:

{% highlight html %}
<script src="http://code.jquery.com/jquery-1.9.1.js"></script>
<script src="http://code.jquery.com/jquery-migrate-1.1.1.js"></script>
{% endhighlight %}

Vale lembrar que o **jQuery 1.9.1** também já está disponível para download via **CDN do Google**. Para maiores informações acesse o [Google Hosted Libraries](https://developers.google.com/speed/libraries/devguide?hl=pt-BR#jquery). Você pode chama-lo em seu site assim:

{% highlight html %}
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
{% endhighlight %}

## API do jQuery Migrate

O plugin **jQuery Migrate** adiciona três novas propriedades ao objeto jquery que podem ser usados na programação para controlar e analisar  seu comportamento:

`jQuery.migrateWarnings`: Esta propriedade é um array com strings das mensagens de alertas que foram geradas pelo código na página, na ordem em que foram geradas. As mensagens são exibidas apenas uma vez no array mesmo se existirem várias ocorrências da mesma, ao menos que `jQuery.migrateReset()` seja chamado.

`jQuery.migrateMute`: Defina essa propriedade como true para evitar advertências do console de que as mensagens na versão de debugging estão sendo geradas. O array `jQuery.migrateWarnings` continua sendo mantido quando esta propriedade é setada, isso permite inspecionar os elementos sem uma saída no console.

`jQuery.migrateTrace`: Defina essa propriedade como false se você quiser os avisos mas não quer vestígios aparecendo no console.

`jQuery.migrateReset()`: Este metódo limpa a lista de mensagens armazenadas no array `jQuery.migrateWarnings`.

Você pode obter maiores informações e contribuir com o desenvolvimento desse plugin acessando o repositório no [Github](https://github.com/jquery/jquery-migrate).

Com tamanha praticidade só não se atualiza quem não quer não é mesmo? Então não fique para trás! Atualize-se, “coloque as mãos na massa” e continue contribuindo para uma web cada vez melhor.

O que está achando das atualizações no jQuery? Gostou do plugin jQuery Migrate? Comente.
