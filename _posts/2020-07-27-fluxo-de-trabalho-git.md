---
layout:     post
title:      "Fluxo de trabalho com Git"
date:       2020-07-27 13:10:00
summary:    Sugestão de fluxo baseada no Gitflow, com pequenas adaptações.
categories: git
---

## Os branches principais

O repositório central possui três branches principais com vida útil infinita:

- `master`
- `staging`
- `develop`

O branch `master` deve sempre refletir um status de pronto para ser usado em produção.

O branch `staging` deve sempre ser muito similar ao `master`. Aqui a equipe de desenvolvimento acredita que o código está pronto para produção, mas serão feitos os últimos testes antes de mandar para produção de fato.

O branch `develop` tem sempre as últimas mudanças concluídas que estão prontas para serem lançadas na próxima versão do projeto. Pode-se pensar nesse branch como um "branch de integração".

Quando o código no branch `develop` atinge um ponto estável e está pronto para ser lançado na próxima versão, nós fazemos o merge dele no branch `staging`. Veremos detalhes sobre **como fazer esse merge** mais adiante. 

Vale notar que consideramos cada merge feito no branch `master` como sendo o lançamento de uma nova versão de produção.

## Branches de apoio

Ao lado dos branches principais, `master`, `staging` e `develop`, nosso modelo de desenvolvimento usa uma variedade de "branches de apoio" para possibilitar o desenvolvimento paralelo entre os membros da equipe, facilitar o acompanhamento de novas features, se preparar para lançamentos de versões de produção e ajudar a corrigir rapidamente bugs encontrados em produção. Diferentemente dos branches principais, esses branches de apoio sempre têm um tempo de vida útil limitado, pois serão removidos eventualmente.

Os tipos de branches de apoio que usamos são:

- `feature` branches
- `release` branches
- `hotfix` branches

Cada um desses branches tem um propósito específico e está sujeito a **regras estritas** sobre quais branches devem se originar e quais branches devem ser seus destinos de merge.

## Branches de feature

**Devem ser criados a partir de:** 
- `develop`

**Devem dar merge de volta em:**
- `develop`

**Convenção de nomenclatura:**
- `feature/*`

Branches `feature/*` são usados para desenvolver novas features que serão incorporadas em um lançamento futuro seja a curto ou longo prazo. A essência de um branch de feature é que ele existe enquanto a feature estiver em desenvolvimento, mas eventualmente será mesclado de volta ao branch `develop` (para que possa adicionar definitivamente o novo recurso à próxima versão) **ou** descartado (no caso de um experimento que deu errado por exemplo).

### Criando um branch de feature

```bash
git checkout develop && git pull

git checkout -b feature/my-feature-name
```

### Incorporando uma feature finalizada em develop

```bash
git checkout develop && git pull

git merge --no-ff feature/my-feature-name

git branch -d myfeature

git push
```

Importante notar o uso da flag `--no-ff` aqui. Isso faz que o merge sempre crie um novo commit, mesmo que a operação possa ser feita em modo [fast-forward](https://git-scm.com/docs/git-merge#_fast_forward_merge). Fazer isso evita a perda de informações sobre a existência histórica de um branch de feature e agrupa todos os commits que adicionaram a feature.

## Branches de release

**Devem ser criados a partir de:** 
- `develop`

**Devem dar merge de volta em:**
- `staging`
- `master`
- `develop`

**Convenção de nomenclatura:**
- `release/v*.*.*`

Branches de release dão suporte à preparação de uma nova versão que será liberada em produção. Permitem que sejam feitos pequenos ajustes de última hora (typos, code style, etc) e também correções de bug menores. Fazer esses ajustes no branch release é necessário pois mantém o branch `develop` sempre limpo e pronto para receber novas features que o restante da equipe estará trabalhando.

O branch release deve ser criado toda vez que o branch `develop` atinge um estado que a equipe considera que está pronto para a nova versão a ser publicada. Todas as features dessa nova versão devem já estar concluídas e mescladas em `develop`, a as features incompletas, que estão sendo desenvolvidas para uma outra versão futura devem esperar até que o branch release seja criado antes de serem mescladas em `develop`.

No momento que um branch release é criado, é onde definimos o número da versão que será lançada. Antes disso, o branch `develop` reflete o estado das mudanças para a "próxima versão", mas ainda não sabíamos se essa "próxima versão" seria `v0.2.0` ou `v1.0.0`, por exemplo. A partir do momento que o release é criado, esse número é então determinado com base nas [regras de versionamento do projeto](https://semver.org/).

### Criando um branch de release

Branches `release/*` são criados a partir do branch `develop`. Por exemplo, digamos que a versão `v1.1.5` é a versão atual de produção e temos uma nova versão a ser lançada. O estado de `develop` é pronto para a "próximo versão" e decidimos que essa versão será a `v1.2.0` (em vez de `v1.1.6` ou `v2.0.0`). Então, criamos o branch de `release/*` e damos um nome à ele, refletindo o número da nova versão:

```bash
git checkout develop && git pull

git checkout -b release/v1.2.0
```

Após criar esse branch, a primeira coisa que deve ser feita é mudar o número da versão (por exemplo no `package.json` para projetos Node.js) e commitar essa mudança.

Esse novo branch pode existir por um tempo, até que essa versão seja lançada definitivamente. Durante esse período, correções de bugs podem ser aplicadas neste branch (e não no branch `develop`). A adição de novas features grandes aqui é estritamente proibida. Eles devem ser mesclados em `develop` e, portanto, aguardar para o próximo lançamento.

### Finalizando um branch de release

Quando o branch de release está pronto para se tornar um release real, algumas ações precisam ser executadas. Primeiro, o branch de release é mesclado em `staging`, para que possam ser feitos todos os últimos testes necessários pela equipe de desenvolvimento e/ou QA. Após tudo ter sido devidamente testado, o release é mesclado no branch `master` e deverá ser criado uma tag com o respectivo número da versão. Por fim, essas mudanças feitas no branch `release` devem ser mescladas em `develop`, dessa forma os próximos releases futuros também terão os ajustes que foram feitos.

**Passo 1:** Publicando em `staging`.

```bash
git checkout staging && git pull

git merge --no-ff release/v1.2.0

git push
```

**Passo 2:** Após testar em `staging`, lançamos em produção fazendo merge em `master` e criando uma tag.

```bash
git checkout master && git pull

git merge --no-ff release/v1.2.0

git tag -a v1.2.0

git push --tags
```

**Passo 3:** Após lançar em produção, mesclamos as alterações de volta em `develop`.

```bash
git checkout develop && git pull

git merge --no-ff release/v1.2.0

git push
```

Aqui pode ser que dê conflito por ter mudado número de versão. Após resolver e commitar, finalmente podemos remover o branch de release:

```bash
git branch -d release/v1.2.0
```

## Branches de hotfix

**Devem ser criados a partir de:** 
- `master`

**Devem dar merge de volta em:**
- `master`
- `staging`
- `develop`

**Convenção de nomenclatura:**
- `hotfix/*`

Quando um erro crítico em uma versão de produção deve ser resolvido imediatamente, um branch `hotfix/*` deve ser criado a partir dessa versão em produção. A essência é que o trabalho dos membros da equipe (no branch `develop`) possa continuar, enquanto outra pessoa está preparando uma correção rápida para o problema identificado em produção.

### Criando um branch de hotfix

```bash
git checkout master && git pull

git checkout -b hotfix/some-bug
```

### Finalizando um branch de hotfix

```bash
git checkout master && git pull

git merge --no-ff hotfix/some-bug

git tag -a v1.2.1

git push --tags
```

Incorpore a correção em `staging` e `develop` também:

```bash
git checkout staging && git pull

git merge --no-ff hotfix/some-bug

git push

git checkout develop && git pull

git merge --no-ff hotfix/some-bug

git push
```

**Observação:** Quando existe um branch de release ativo, as alterações do hotfix precisam ser mescladas nesse branch de release, ao invés do branch `develop`. (Porém se o trabalho em `develop` exigir imediatamente essa correção e não puder esperar a conclusão do branch de release, poderá ser feito o merge dessa correção em `develop` sem problemas também).

E finalmente podemos remover o branch de hotfix:

```bash
git branch -d hotfix/some-bug
```
