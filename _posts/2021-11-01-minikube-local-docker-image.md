---
layout:     post
title:      Imagem Docker local no minikube
date:       2021-11-01 16:41:00
summary:    Como usar Imagem Docker local em Cluster minikube
categories: cloud-computing
---

Para iniciar um Pod, o Kubernetes primeiro baixa a Imagem Docker de algum registry, que por padrão, geralmente é o Docker Hub.

Porém, para testes em ambiente local, durante o processo de desenvolvimento, pode ser que você queira subir rapidamente um Deployment, e ver seus Pods funcionando <del>ou não xD</del>, sem precisar fazer push e pull da Imagem para o registry toda hora.

Neste post, mostro como usar uma Imagem local em um Cluster [minikube](https://minikube.sigs.k8s.io/docs/).

## Reutilizando o Docker Daemon

Para não precisar fazer push da Imagem em um registry, podemos reutilizar o Docker Daemon do minikube, e fazer o build direto nele. Podemos fazer isso com o comando [`docker-env`](https://github.com/kubernetes/minikube/blob/0c616a6b42b28a1aab8397f5a9061f8ebbd9f3d9/docs/minikube_docker-env.md).

Rode o comando:

```bash
eval $(minikube docker-env)
```

Agora essa aba do seu terminal estará se comunicando com o Docker Daemon do minikube. 

Com isso, você pode rodar um `docker build` e sua Imagem será criada no ambiente do minikube.

```bash
docker build -t my-app:latest .
```

E no arquivo YAML do seu Deployment / Pod, fica algo assim:

```yaml
containers:
- name: my-app
  image: my-app:latest
  imagePullPolicy: Never
```

Aqui atente-se ao uso da opção [`imagePullPolicy`](https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy). Precisamos passá-la como `Never`, para que o Kubernetes não vá tentar buscar a imagem em um registry remoto.

**Atenção!** Quando não for mais usar o Docker Daemon do minikube, lembre-se de voltar ao seu host padrão. Para isso, rode o seguinte comando:

```bash
eval $(minikube docker-env -u)
```

### Referências

- [Minikube: Reusing the Docker daemon](https://github.com/kubernetes/minikube/blob/0c616a6b42b28a1aab8397f5a9061f8ebbd9f3d9/README.md#reusing-the-docker-daemon)
