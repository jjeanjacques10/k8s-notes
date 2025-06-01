# Serviços

Permite a criação de uma arquiteura de microserviços, onde cada serviço é independente e pode ser escalado separadamente.

- Ele abre uma porta para o mundo externo, permitindo que os serviços sejam acessados de fora do cluster.
- É criada uma portas para cada serviço
- Acesso via IP do cluster e porta do serviço

| Tipo de Serviço  | Descrição                                                                               |
| ---------------- | --------------------------------------------------------------------------------------- |
| **NodePort**     | Expõe uma porta específica em cada nó do cluster.                                       |
| **LoadBalancer** | Cria um balanceador de carga externo para distribuir o tráfego entre os nós do cluster. |
| **ClusterIP**    | Tipo padrão; cria um IP interno para o serviço, acessível apenas dentro do cluster.     |

Exemplos: 

- NodePort para acessar o serviço `frontend-svc` na porta 58002.
- ClusterIP para comunicação interna entre serviços como `backend-svc` e `database-svc`.


## Acessar IP do cluster


- Para acessar o IP do cluster, você pode usar o comando:

``` bash
minikube ip
```

- Para acessar o serviço `frontend-svc`, você pode usar o comando:

``` bash
minikube service frontend-svc --url
# http://127.0.0.1:58002
```

- Exemplos de arquivos no projeto:
  - [`services/frontend-svc.yaml`](./services/frontend-svc.yaml)


