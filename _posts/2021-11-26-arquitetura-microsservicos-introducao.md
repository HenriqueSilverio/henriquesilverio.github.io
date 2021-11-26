---
layout:     post
title:      "Arquitetura de Microsserviços: Considerações iniciais"
date:       2021-11-26 16:26:00
summary:    Ideias centrais por trás dos microsserviços, e algumas razões pelas quais esta arquitetura vem sendo amplamente adotada.
categories: cloud-computing
---

# Arquitetura de Microsserviços: Considerações iniciais

Microsserviços. Microsserviços everywhere.

Neste artigo trago algumas ideias centrais que estão por trás dos famigerados microsserviços, e algumas razões pelas quais esta arquitetura vem sendo amplamente adotada.

Os tópicos aqui, foram extraídos do livro "[Building Microservices: Designing Fine-Grained Systems](https://www.amazon.com.br/dp/1492034029/)", são destaques que fiz em minha leitura, e considero de grande valor para reflexão.

### Um olhar de relance sobre microsserviços

Microsserviços são serviços que podem ser lançados de maneira independente, modelados em torno de um domínio de negócios.

"Olhando de fora", um microsserviço é tratado como uma espécie de "caixa-preta". Detalhes de implementação são encapsulados e ficam completamente ocultos do "mundo externo". Suas utilidades são expostas através da rede, independente de qual seja o protocolo utilizado: REST APIs, filas de mensageria, etc.

### Conceitos chave de microsserviços

**Implantação independente:** Devemos poder implantar e lançar mudanças de um microsserviço em produção, sem ter que implantar absolutamente mais nada além dele próprio, ou seja, totalmente desacoplado de outros microsserviços, bem como recursos como banco de dados compartilhados, etc.

**Modelado em torno de um domínio de negócios:** Para um contexto mais amplo, aqui estamos nos referindo a conceitos apresentados por Eric Evans no livro [Domain-Driven Design: Tackling Complexity in the Heart of Software](https://www.amazon.com/gp/product/0321125215/). Nossos microsserviços devem ser "pequenas fatias" que cobrem uma determinada funcionalidade de negócio, de ponta-a-ponta. Em uma arquitetura de microsserviços bem modelada, nós priorizamos uma alta coesão com as funcionalidades de negócio ao invés de funcionalidades técnicas.

**Donos de seu próprio estado:** Microsserviços devem evitar o uso de bancos de dados compartilhados. Isso claramente, nos permite separar melhor as implementações internas dos contratos externos. Uma boa analogia aqui, é lembrar da prática de encapsulamento, comumente aplicada em programação orientada a objetos. Então, não compartilhe banco de dados, a menos que você realmente precise.

**Tamanho:** Podemos dizer que um microsserviço deve manter seu tamanho no limite em que ele pode ser entendido facilmente. Porém, essa questão não deve ser nosso foco. Ao invés disso, devemos nos perguntar algo como: "Com até quantos microsserviços consigo lidar?" Lembre-se que, microsserviços trazem consigo uma série de novas complexidades e desafios. Outra questão de maior importância: "Como irei definir os limites de meus microsserviços, para que eu possa tirar máximo proveito dos mesmos, sem criar uma horrível bagunça totalmente acoplada?" Buscando essas respostas, a questão sobre "tamanho ideal" fica em segundo plano, e será resolvida naturalmente.

**Flexibilidade:** Embora a ideia de "microsserviços em tudo" pareça ser tentadora, devemos nos lembrar de que isso tem um custo. E é necessário ponderar, e decidir até onde esse custo realmente vale as opções que iremos escolher. De forma geral, em uma arquitetura de microsserviços temos um grande aumento de flexibilidade, porém, aumentamos também os possíveis pontos de dor. Pensando nisso, uma adoção incremental, costuma ser o mais recomendado.

**Alinhamento da Arquitetura e Organização:** No passado, a "arquitetura de três camadas" tornou-se uma escolha "padrão" em quase todo projeto. Se queremos facilitar mudanças, precisamos repensar essa "forma padrão" de agrupar / organizar código. O objetivo aqui é optar por maior coesão com as funcionalidades de negócio ao invés de tecnologias utilizadas. Cada microsserviço pode sim conter um mix das conhecidas três camadas, porém, isso é apenas uma preocupação interna de implementação do microsserviço, que, em caso de mudanças necessárias, não irá impactar nada além dele próprio.

### Conclusão

Solução para tudo? Não! Novos desafios? Muitos! Porém, **quando os conceitos chave são devidamente entendidos e implementados**, a escolha por microsserviços pode sim trazer uma arquitetura produtiva, com grandes benefícios para organizações como um todo e a seus usuários.