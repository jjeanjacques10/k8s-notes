# Notas - Orquestração de Containers com Kubernetes

## MiniKube

- É uma ferramenta que permite executar um cluster Kubernetes localmente

### Comandos

- Inicia o cluster
- Para parar o cluster
- Reinicia o cluster
- Deleta o cluster

``` bash
minikube start
minikube stop
minikube restart
minikube delete
```

## PODS

- Sempre são 1:1 para com o container
- Pod é a menor unidade de execução em Kubernetes
- Pod é um ou mais containers que compartilham o mesmo IP, porta e volume

### Comandos Pods

- Retornam o status dos pods

``` bash
kubectl get pods -o wide
```

- Retornam o status dos pods com mais detalhes

``` bash
kubectl describe pods
```

- Cria um pod com o nome nginx e a imagem nginx
  - A imagem é baixada do Docker Hub

``` bash
kubectl run nginx --image nginx
```

- Delete all pods

``` bash
kubectl delete --all pods
```

## Arquivo de definição do Kubernetes

- É um arquivo YAML que define o estado desejado do cluster
- Exemplos de arquivos no projeto:
  - [`pods/pod.yaml`](pods/pod.yaml): Exemplo de Pod simples
  - [`pods/nginx.yaml`](pods/nginx.yaml): Pod rodando o Nginx

``` yaml
apiVersion: v1
kind:
metadata:

spec:
```

Exemplo de um arquivo de definição do Kubernetes para criar um pod:

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
    tier: frontend
spec:
  containers:
    - name: nginx
      image: nginx
```

- Comando para criar o pod a partir do arquivo de definição

``` bash
kubectl create -f .\pod.yaml
```

## Replication Controller e ReplicaSet

- São recursos do Kubernetes que garantem que um número específico de réplicas de um pod esteja em execução a qualquer momento
- Garante a alta disponibilidade e escalabilidade da aplicação
- Exemplo de arquivo no projeto:
  - [`replicaset/rs1.yaml`](replicaset/rs1.yaml): Exemplo de ReplicaSet

**Replication Controller** vs **ReplicaSet**

- O Replication Controller é o antecessor do ReplicaSet

| Característica | Replication Controller        | ReplicaSet                |
| -------------- | ----------------------------- | ------------------------- |
| apiVersion     | v1                            | apps/v1                   |
| Selector       | Não suporta rótulos complexos | Suporta rótulos complexos |

- Comando para listar os ReplicaSets

``` bash
kubectl get replicasets
```

- Atualizar o scale do ReplicaSet

``` bash
kubectl scale --replicas=3 -f .\replicaset.yaml # Pelo nome do arquivo
kubectl scale --replicas=3 replicaset nginx # Pelo nome do ReplicaSet
```

## Deployments

- É um recurso do Kubernetes que gerencia a criação e atualização de novas versões de aplicações
- **rolling update**
  - É uma estratégia de atualização que permite atualizar a aplicação sem causar downtime
- Na criação do Deployment nós temos um replicaSet criado automaticamente

### Comandos Deployments

- Cria um Deployment a partir de um arquivo de definição

``` bash
kubectl create -f .\deployment.yaml
```

- Lista os Deployments

``` bash
kubectl get deployments
```

### Rollout - Versionamento

- É o processo de atualização de uma aplicação em Kubernetes
- Apartir do Deployment, é gerada uma nova revisão para caso aconteça algum problema seja possível reverter a versão anterior

### Comandos Rollout

- Consultar o histórico de rollouts

``` bash
kubectl rollout history deployment/frontend-dp
```

### Estratégias de Deployments

- **Rolling Update**: Atualiza os pods gradualmente, garantindo que sempre haja uma versão anterior em execução. (Padrão)
- **Recreate**: Para todos os pods antes de criar novos, causando downtime. (Não recomendado para produção)
  - Irá causar downtime, pois todos os pods serão parados antes de iniciar os novos.
- **Blue/Green**: Cria uma nova versão do aplicativo ao lado da versão atual e, em seguida, alterna o tráfego para a nova versão.

Caso tenhamos problemas iremos realizar o rollback para a versão anterior

``` bash
kubectl rollout undo deployment/frontend-dp
```

## Dicas

- Listar todos os recursos do Kubernetes

``` bash
kubectl get all
```

## Referências

- [Geek University - Orquestração de Containers com Kubernetes](https://itau.udemy.com/course/orquestracao-de-containers-com-kubernetes)