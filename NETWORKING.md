## Networking com Kubernetes

- O recomendado é cada serviço ter seu próprio container, para facilitar a escalabilidade e manutenção.

- Após executar o camando `kubectl get all`, podemos ver as informações do cluster incluindo o IP do serviço Kubernetes (10.96.0.1)

``` bash
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   3h35m
```

- Os PODS tem o seu próprio IP, que pode ser visto com o comando `kubectl get pods -o wide`.
  - O ideal não é utilizar o IP do POD diretamente, pois ele pode mudar a qualquer momento.
- KubeDNS é o serviço de DNS do Kubernetes, que resolve os nomes dos serviços para os IPs correspondentes.

### Namespaces

- Namespaces são usados para dividir os recursos do cluster em grupos lógicos.
- Equivalente aos packages em Java ou módulos em Python para organizar o código.

### Comandos de Namespaces

- Listar todos os namespaces:

```bash
kubectl get ns
```

- Criar um namespace chamado `frontend`:

```bash
kubectl create namespace frontend
```

- Listar os pods no namespace `frontend`:

```bash
kubectl get pods -n frontend
```

## Conectando no Pod

- Para conectar em um Pod, usamos o comando `kubectl exec`:

```bash
kubectl exec -it <nome-pode> -- bash
```