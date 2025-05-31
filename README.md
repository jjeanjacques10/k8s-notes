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

![[Pasted image 20250531174833.png]]
![[Pasted image 20250531175002.png]]

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

