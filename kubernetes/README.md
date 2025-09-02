# ⛵ Guia de Comandos Kubernetes (k8s): Navegue seu Cluster com Confiança

Kubernetes (ou k8s) é o sistema de orquestração de contêineres que se tornou o padrão da indústria. Ele automatiza o deploy, o escalonamento e a gestão de aplicações em contêineres.

Este guia foca nos comandos essenciais do `kubectl` e `minikube` para você gerenciar seu ambiente de forma eficaz.

---

### 🏡 Gerenciando seu Cluster Local com Minikube

Minikube é a ferramenta perfeita para rodar um cluster Kubernetes de nó único na sua máquina local para fins de desenvolvimento e aprendizado.

| Comando | O que faz? |
| :--- | :--- |
| **`minikube start`** | **Iniciar o cluster:** Cria e inicia a máquina virtual com seu ambiente Kubernetes local. |
| **`minikube stop`** | **Parar o cluster:** Pausa o cluster sem apagar os recursos que você criou. |
| **`minikube delete`** | **Apagar o cluster:** Para e apaga completamente o cluster local, limpando todos os dados. |
| **`minikube dashboard`**| **Abrir o Dashboard:** Abre a interface gráfica do Kubernetes no seu navegador. |
| **`minikube service`**| **Acessar um serviço:** Obtém o endereço de um serviço rodando no cluster para que você possa acessá-lo localmente. |
| **`minikube status`** | **Verificar o status:** Mostra o estado atual do seu cluster Minikube. |

**Exemplo de Uso:**
```bash
# Obtém a URL para acessar o serviço 'meu-app-service'
minikube service meu-app-service --url
```

---

### 🔍 Inspecionando o Cluster (O Básico do `kubectl`)

Uma vez que seu cluster está rodando, use o `kubectl` (pronuncia-se "kubecutl" ou "kubecontrol") para interagir com ele.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`kubectl get <recurso>`** | **Listar recursos:** O comando mais comum. Lista os recursos de um tipo específico. | `kubectl get pods` ou `kubectl get services` |
| **`kubectl get all`** | **Listar tudo:** Mostra um resumo dos recursos mais importantes (Pods, Services, Deployments) no namespace atual. | `kubectl get all` |
| **`kubectl describe <recurso>`** | **Descrever um recurso:** Exibe informações **detalhadas** sobre um recurso específico, incluindo eventos e status. Essencial para debugging! | `kubectl describe pod <nome-do-pod>` |
| **`kubectl logs <pod>`** | **Ver logs de um Pod:** Mostra os logs do contêiner principal de um Pod. Use `-f` para acompanhar em tempo real. | `kubectl logs -f <nome-do-pod>` |

> **Conceitos Essenciais:**
> * **Pod:** A menor unidade do Kubernetes. Geralmente contém um único contêiner. É efêmero.
> * **Deployment:** Controla um conjunto de Pods idênticos (réplicas). Gerencia atualizações, rollbacks e garante que a quantidade desejada de Pods esteja sempre rodando.
> * **Service:** Expõe um conjunto de Pods através de um ponto de acesso de rede estável (um IP e um nome DNS), permitindo a comunicação entre eles e com o exterior.

---

### 🚀 Deployando e Gerenciando Aplicações

Aqui estão os comandos para criar, atualizar e remover recursos no seu cluster.

| Comando | O que faz? |
| :--- | :--- |
| **`kubectl apply -f`** | **Aplicar uma configuração:** A forma **recomendada** de criar ou atualizar recursos a partir de um arquivo YAML. Se o recurso não existe, ele cria. Se já existe, ele atualiza. |
| **`kubectl create -f`** | **Criar um recurso:** Cria um recurso a partir de um arquivo YAML, mas falhará se o recurso já existir. |
| **`kubectl delete`** | **Remover recursos:** Apaga um ou mais recursos do cluster, seja por nome, por arquivo ou usando seletores. |

**Exemplos de Uso:**

```bash
# Criar/atualizar recursos de um arquivo de manifesto
kubectl apply -f meu-app.yml

# Apagar um deployment específico
kubectl delete deployment meu-app-deployment

# Apagar todos os pods no namespace atual
kubectl delete pod --all
```

> **Dica de Ouro:** `apply` vs `create`
> Prefira `kubectl apply`. Ele é declarativo (você diz *o que quer* no YAML) e idempotente (pode ser executado várias vezes sem efeitos colaterais), o que o torna ideal para automação e pipelines de CI/CD.

---

### 🔧 Interagindo com Pods (Debugging Avançado)

Precisa entrar em um contêiner ou expor uma porta para testar algo?

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`kubectl exec -it`** | **Executar um comando em um Pod:** Abre um terminal interativo (`-it`) dentro de um contêiner em execução. Similar ao `docker exec`. | `kubectl exec -it <nome-do-pod> -- /bin/sh` |
| **`kubectl port-forward`** | **Redirecionar uma porta:** Cria um túnel de comunicação entre sua máquina local e um Pod, permitindo acessar a aplicação diretamente via `localhost`. | `kubectl port-forward <nome-do-pod> 8080:80` |