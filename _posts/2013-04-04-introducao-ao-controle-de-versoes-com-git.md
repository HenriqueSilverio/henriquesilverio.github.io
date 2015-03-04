---
layout:     post
title:      Introdução ao controle de versões com Git
date:       2013-04-04 19:00:00
summary:    Vantagens de se utilizar um bom sistema de controle de versão e também como instalar o Git nos ambientes Linux, Windows e Mac.
categories: git-e-github
---

O Git foi criado por Linus Torvalds e originou-se durante o processo de desenvolvimento do Kernel do Linux. Git é um sistema open source para controle de versão distribuído e gerenciamento de código fonte projetado para lidar com os mais diversos tipos de projetos, desde os menores até os mais complexos, com velocidade e eficiência.

Neste artigo irei mostrar algumas vantagens de se utilizar um bom sistema de controle de versão e também como instalar o Git nos ambientes Linux, Windows e Mac. Não entraremos em detalhes sobre a utilização de comandos do Git para criar e gerenciar repositórios. Isso fica para um próximo artigo.

## Por que usar um controle de versão?

Por mais que muitos desenvolvedores não levem isso em conta, fazer uso de um bom sistema de controle de versões (VCS) é de extrema importância pois previne diversas dores de cabeça durante e após o processo de desenvolvimento de qualquer tipo de sistema.

Quem nunca passou horas debugando um código que você mesmo escreveu para descobrir o que certas funções fazem?  E que dizer quando você precisa fazer alterações em um mesmo arquivo que seu colega de trabalho está editando? Você espera até que ele termine e suba o arquivo no FTP para só depois poder fazer a sua parte? Isso é muito ruim, e sempre acontece.

Ou que dizer se você passa a madrugada inteira desenvolvendo, e quando chega no outro dia percebe que um estágiario fez uma alteração que mandou todo seu trabalho pros ares? Triste não? Mas não tem jeito… pode começar a desenvolver tudo de novo e se preciso, virar a madrugada inteira desenvolvendo novamente, pois o prazo é curto e o cliente está no seu pé.

Utilizando um bom VCS, você passa a ter um controle muito maior sobre seu código, se precisar restaurar versões anteriores do seu projeto, poderá fazer isso em questão de segundos e situações como essas que citei nos exemplos a cima não irão ocorrer novamente.

## Principais vantagens do Git

**Branching e Merging:** Essas talvez sejam umas das características mais interessantes do Git. Um branch é como se fosse um ramo do seu projeto. Sempre que quiser incluir e testar novas features, você pode criar um novo branch e mandar seus commits para la. Após terminar todos os testes, você pode rapidamente dar um mergin para juntar seu novo branch com o branch principal do projeto.  E caso algo não saia conforme o esperado, você pode ir ajustando o código separadamente sem prejudicar o projeto que está rodando em produção e se precisar retirar essa feature, basta excluir o branch correspondende e o seu sistema não será prejudicado.

**Pequeno e muito rápido:** Git sai na frente com uma vantagem enorme em questão de velocidade com relação aos outros VCS centralizados que precisam obrigatóriamente se comunicar com um servidor. Velocidade tem sido o foco principal do Git desde o inicio de seu desenvolvimento.

A nível de comparação, veja os gráficos abaixo (retirados do site oficial do Git) que mostram os resultados de um benchmarking feito entre o Git e Subversion, que é um sistema de controle de versões centralizado bem conhecido no mercado:

<div style="text-align: center;">
    <img src="/images/git-benchmarks.jpg" alt="Git Benchmarks">
</div>

**Distribuido:** Git é um sistema de controle de versões distribuido, ou seja, ao invés de fazer um checkout de determinadas partes do código fonte, você faz um clone do repositório inteiro. Com isso, quando se trabalha em equipe, cada membro da equipe terá um clone fiel do projeto inteiro em sua máquina (múltiplos backups), e caso seja necessário restaurar um backup, isso será muito fácil e rápido. Sendo assim, é praticamente impossível de se perder partes do código fonte por falta de um backup, a não ser que exista apenas um único clone do repositório e este seja deletado por alguém. Além disso, o Git permite que você tenha diversos modelos diferentes de workflow, como por exemplo um projeto onde um ou mais administradores gerenciam o repositório principal do projeto e todos os outros desenvolvedores trabalham a partir de um clone desse repositório.

## Instalando Git em ambiente Linux

Vamos agora fazer a instalação do Git em uma das versões mais populares do Linux que é o Ubuntu. A instalação é bem simples, via terminal usando o gerenciador de pacotes apt-get. No seu terminal digite:

```
sudo apt-get install git-core git-svn ssh
```

Como o próprio comando diz, git-core irá instalar o core do Git em sua máquina. O trecho git-svn instala uma ferramenta que permite que você use Git como um cliente válido para um servidor Subversion, com isso você pode usar todos os recursos locais do Git e fazer um push para um servidor Subversion, como se estivesse usando o Subversion localmente. Por fim, instalamos o ssh para podermos gerar um par de chaves para nosso usuário do Git mais tarde.

Tecle enter e confirme a instalação teclando Y.

Após a instalação, para verificar se está tudo ok, execute o comando `git --version` e será gerada uma mensagem dizendo qual versão do Git você está rodando atualmente.

Caso ainda não tenha, você deverá gerar um par de chaves SSH. Para fazer isso é também muito simples. Execute o seguinte comando no terminal:

```
ssh-keygen -t rsa
```

Após executar esse comando, será gerado um diretório .ssh na raiz da sua instalação do Git. Dentro desse diretório, você terá dois arquivos: `id_rsa` e `id_rsa.pub`. Esses arquivos contém respectivamente as suas chaves ssh privada e pública. Guarde-os com cuidado.

## Instalando Git em ambiente Windows

Existem diversas maneiras de se instalar o Git em ambiente Windows, mas a forma mais robusta e recomendada atualmente é através do instalador **msysgit**.

Acesse o site [http://code.google.com/p/msysgit](http://code.google.com/p/msysgit) clique na aba “Downloads” e baixe a versão mais recente do instalador full, mesmo que ele esteja como “preview”. Execute o seu instalador **msysgit** e preste atenção em alguns detalhes durante a instalação.

Acho interessante e recomendo que você também marque a opção para integrar opções ao menu de contexto do Windows Explorer. Isso lhe dará um atalho de acesso rápido ao **Git Bash** em qualquer lugar que você esteja mais tarde. Também recomendo que você habilite a opção para utilizar fontes TrueType em todo o console do Windows, não apenas para o **Git Bash**. Faça como na figura abaixo:

<div style="text-align: center;">
    <img src="/images/git-em-windows-1.jpg" alt="Intalando Git no Windows">
</div>

Na próxima tela da instalação, marque a terceira opção. Fazendo isso você irá integrar as ferramentas Unix em todas as janelas de command prompt do Windows e poderá utilizar o Git não somente através do “terminal” Git Bash, mas também no command prompt padrão do Windows.

<div style="text-align: center;">
    <img src="/images/git-em-windows-2.jpg" alt="Intalando Git no Windows">
</div>

Por fim, para evitar conflitos entre arquivos que poderão ser editados por desenvolvedores em ambientes diferentes como Linux ou Mac, marque a terceira opção, para que o Git não altere os arquivos do seu projeto durante um check out ou commits.

<div style="text-align: center;">
    <img src="/images/git-em-windows-3.jpg" alt="Intalando Git no Windows">
</div>

Feito isso, agora temos que gerar nosso par de chaves ssh. Para isso abra o Git bash, digite e execute o seguinte comando:

```
ssh-keygen.exe -t rsa
```

<div style="text-align: center;">
    <img src="/images/git-em-windows-4.jpg" alt="Intalando Git no Windows">
</div>

Como você pode ver na figura a cima, o nosso par de chaves ssh foi gerado com sucesso, dentro do diretório .ssh. No meu caso, como eu já tinha um par de chaves, executando esse comando foi possível sobrescreve-las com um novo par de chaves.

Feito isso, você já terminou a **instalação do Git no Windows**, e opicionalmente poderá alterar algumas configurações do terminal para deixa-lo com uma visualização mais agradável, como por exemplo mudar a família, tamanho e cor da fonte, aumentar as dimensões da janela etc. Basta clicar com o botão direito do mouse na barra de título do terminal e acessar o menu “Propriedades”.

# Instalando Git em ambiente Mac

Para instalar o Git no Mac também temos várias opções como o `git-osx-installer` que você pode baixar no site [http://code.google.com/p/git-osx-installer](http://code.google.com/p/git-osx-installer). Ou você pode fazer a instalação através de um gerenciador de pacotes, como o [Mac Port](http://www.macports.org) ou o [Home Brew](https://github.com/mxcl/homebrew).

Caso for utilizar o Mac Port, basta executar o seguinte comando no terminal:

```
sudo port install git-core +svn
```

E caso for utilizar o Home Brew, é ainda mais simples e rápido:

```
brew install git
```

Para checar se a instalação foi realizada com sucesso, o comando é o mesmo que nas outras plataformas:

```
git --version
```

E para criar o par de chaves ssh, faça:

```
ssh-keygen -t rsa
```

## Conclusão

Espero que após ler esse artigo você tenha entendido os principais beneficios de se utilizar o Git, e como instala-lo em seu ambiente de desenvolvimento. Em um próximo artigo pretendo mostrar como você pode dar seus primeiros passos para utilizar o Git, mostrando alguns comandos principais para você iniciar um projeto. Caso tenha curiosidade e queria ir estudando mais desde já, dê uma olhada nos links de referência logo abaixo. Espero que tenha gostado do artigo, e como sempre, críticas e sugestões serão muito bem vindas.

### Referências:

<ul>
    <li><a href="http://git-scm.com/book/pt-br/" target="blank">Git book</a></li>
    <li><a href="http://tableless.com.br/iniciando-no-git-parte-1/" target="blank">Iniciando no Git parte 1</a></li>
    <li><a href="http://blip.tv/akitaonrails/screencast-come-ando-com-git-6074964/" target="blank">Screencast: Começando com Git</a></li>
    <li><a href="http://tableless.com.br/introducao-das-premissas-dos-controles-de-versao/" target="blank">Introdução das premissas dos controles de versão</a></li>
</ul>
