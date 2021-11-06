---
layout:     post
title:      "GitHub Actions: Compartilhar variável entre jobs"
date:       2021-11-06 20:21:00
summary:    Dica para um workflow mais elegante, usando outputs
categories: devops
---

De forma resumida, no GitHub Actions, um Workflow é composto por *N* Jobs, que executam *N* Steps.

Para configurar o Workflow, podemos utilizar [variáveis de ambiente](https://docs.github.com/en/actions/learn-github-actions/environment-variables#about-environment-variables) em três níveis: step (`jobs.<job_id>.steps[*].env`), job (`jobs.<job_id>.env`) e global (`env`).

O problema é que, dessa forma por si só, variáveis definidas em um Job não podem ser acessadas em outro Job subsequente.

Porém, em algum momento, pode ser que você precise fazer isso! 

Por exemplo: um Job que executa alguma lógica para montar uma variável em tempo de build, cujo valor será utilizado nos Jobs seguintes. Pra isso, você precisa compartilhar variável entre Jobs. 

E é aqui que os [`outputs`](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idoutputs) entram em cena.

## Exemplo usando job `outputs`

Para entender melhor, vejamos um exemplo prático!

```yaml
jobs:
  setup:
    runs-on: ubuntu-20.04
    name: "Setup"
    outputs:
      SOMETHING: ${{ steps.example.outputs.SOMETHING }}
    steps:
      id: example
      run: echo "::set-output name=SOMETHING::amazing"
  build:
    needs: setup
    runs-on: ubuntu-20.04
    steps:
      run: echo "SOMETHING coming from previous job ${{ needs.setup.outputs.SOMETHING }}"
```

Note que, no Step `example` do Job `setup`, nós definimos o output assim:

```
echo "::set-output name=${key}::${value}"
```

E exportamos ele para que os outros Jobs possam ler, assim:

```
outputs:
  SOMETHING: ${{ steps.example.outputs.SOMETHING }}
```

Depois, no Job `build`, nós precisamos informar que ele depende do `setup`, e fazemos isso assim:

```
build:
  needs: setup
```

Feito isso, agora podemos ler os `outputs`, através do [contexto `needs`](https://docs.github.com/en/actions/learn-github-actions/contexts#needs-context), assim:

```
${{ needs.setup.outputs.SOMETHING }}
```

E pronto! Com isso temos como compartilhar variáveis entre Jobs diferentes em um Workflow do GitHub Actions. 

Uma "mão na roda" na hora de organizar Workflows mais complexos, evitando repetição de código.

### Referências

- [Environment variables](https://docs.github.com/en/actions/learn-github-actions/environment-variables)
- [`jobs.<job_id>.outputs`](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idoutputs)
- [Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
- [Sharing a variable between jobs](https://github.community/t/sharing-a-variable-between-jobs/16967)
