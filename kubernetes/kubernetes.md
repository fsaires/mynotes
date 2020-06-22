## KUBERNETES

- Rodar Cluster (Local)

```
$ minikube start
```

- Parar Cluster (Local)

```
$ minikube stop
```

- Limpar e apagar Cluster (Local)

```
$ minikube delete
```

- Controlar o cluster (Local)

```
$ kubectl
```

- Criar POD ou DEPLOYMENT no cluster (Local)

```
$ kubectl create -f NOMEARQUIVO.YML
```

- Receber info sobre os PODs

```
$ kubectl get pods
$ kubectl describe pods <NOME_DO_POD>
```

- Receber info sobre os DEPLOYMENTs

```
$ kubectl get deployments
$ kubectl describe deployments <NOME_DO_DEPLOYMENT>
```

- Receber info sobre os SERVICEs

```
$ kubectl get services
$ kubectl describe services <NOME_DO_SERVICE>
```

- Remover PODs

```
$ kubectl delete pod --all
$ kubectl delete pod <NOME_DO_POD>
```

- Remover DEPLOYMENTs

```
$ kubectl delete deployment --all
$ kubectl delete deployment <NOME_DO_DEPLOYMENT>
```

- Remover SERVICEs

```
$ kubectl delete service  --all
$ kubectl delete service <NOME_DO_SERVICE>
```

## MINIKUBE

- Dashboard

```
$ minikube dashboard
```

- URL do serviço 

```
$ minikube service service-aplicacao --url
```