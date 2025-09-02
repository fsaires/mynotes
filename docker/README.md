# 🐳 Guia de Comandos Docker: Do Básico ao Avançado! 🚀

Olá, marinheiro de primeira viagem (ou capitão experiente)! Navegar no oceano do Docker pode ser desafiador, mas com os comandos certos, você se tornará um mestre dos containers.

Este guia foi atualizado para ser mais didático e visual, te ajudando a encontrar o que precisa rapidamente. Vamos zarpar!

---

### 🚢 Gerenciando Containers (O Coração do Docker)
Aqui estão os comandos para interagir com seus containers no dia a dia.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`docker ps`** | **Listar containers ativos:** Mostra apenas os containers que estão em execução no momento. | `docker ps` |
| **`docker ps -a`** | **Listar TODOS os containers:** Exibe todos os containers, incluindo os que estão parados. Super útil para limpeza! | `docker ps -a` |
| **`docker start`** | **Iniciar um container:** "Acorda" um container que estava parado. | `docker start <ID_OU_NOME_DO_CONTAINER>` |
| **`docker stop`** | **Parar um container:** Envia um sinal para parar a execução de um container de forma segura. | `docker stop <ID_OU_NOME_DO_CONTAINER>` |
| **`docker stop $(docker ps -q)`** | **Parar TODOS os containers:** Um comando poderoso para parar todos os containers em execução de uma só vez. | `docker stop $(docker ps -q)` |
| **`docker rm`** | **Remover um container:** Apaga um container que **não está em execução**. Para forçar a remoção de um em execução, use a flag `-f`. | `docker rm <ID_OU_NOME_DO_CONTAINER>` |
| **`docker inspect`** | **Inspecionar um container:** Fornece um mar de informações detalhadas sobre o container em formato JSON (redes, volumes, etc). | `docker inspect <ID_OU_NOME_DO_CONTAINER>` |
| **`docker exec -it`** | **Entrar em um container:** A forma **mais recomendada** de abrir um terminal interativo (`-it`) dentro de um container que já está rodando. | `docker exec -it <ID_OU_NOME> /bin/bash` |
| **`docker attach`** | **Anexar a um container:** Conecta seu terminal ao processo principal do container. **Cuidado:** se você sair com `Ctrl+C`, o container pode parar! | `docker attach <ID_OU_NOME_DO_CONTAINER>` |
| **`docker port`** | **Verificar portas mapeadas:** Mostra como as portas do container estão mapeadas para as portas da sua máquina. | `docker port <ID_OU_NOME_DO_CONTAINER>` |
| **`docker cp`** | **Copiar arquivos:** Copia arquivos e pastas entre sua máquina e o container (nos dois sentidos!). | `docker cp arquivo.txt meu_container:/app/` |

---

### 🖼️ Gerenciando Imagens (Os Moldes dos Seus Containers)
Imagens são os blueprints. Veja como gerenciá-las.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`docker pull`** | **Baixar uma imagem:** Faz o download de uma imagem do Docker Hub (ou outro registro). | `docker pull ubuntu:latest` |
| **`docker images`** | **Listar imagens locais:** Mostra todas as imagens que você já baixou para a sua máquina. | `docker images` |
| **`docker build -t`** | **Construir uma imagem:** Cria uma nova imagem a partir de um `Dockerfile`. O `-t` define o nome e a tag (`<nome>:<versao>`). | `docker build -t minha-app:1.0 .` |
| **`docker tag`** | **Criar tag para uma imagem:** Aplica um novo "rótulo" a uma imagem existente. Essencial para versionar e enviar ao registro. | `docker tag <ID_DA_IMAGEM> meu-usuario/minha-app:1.0` |
| **`docker push`** | **Enviar imagem para o Hub:** Publica sua imagem em um registro como o Docker Hub para compartilhar com o mundo. | `docker push meu-usuario/minha-app:1.0` |
| **`docker rmi`** | **Remover uma imagem:** Apaga uma imagem da sua máquina. A imagem não pode estar sendo usada por nenhum container. | `docker rmi <ID_DA_IMAGEM>` |
| **`docker commit`** | **Criar imagem de um container:** Salva o estado atual de um container como uma nova imagem. Útil para debug, mas o ideal é sempre usar um Dockerfile. | `docker commit <ID_DO_CONTAINER> nova-imagem:debug` |
| **`docker save`** | **Salvar imagem em um arquivo:** Exporta sua imagem para um arquivo `.tar`, facilitando o backup ou a transferência manual. | `docker save minha-app:1.0 > minha-app.tar` |
| **`docker load`** | **Carregar imagem de um arquivo:** Importa uma imagem a partir de um arquivo `.tar`. | `docker load < minha-app.tar` |

---

### 🎼 Docker Compose (Orquestrando Múltiplos Containers)
Para projetos com vários serviços (ex: app + banco de dados), o `docker-compose` é seu melhor amigo.

| Comando | O que faz? |
| :--- | :--- |
| **`docker-compose up`** | **Iniciar os serviços:** Sobe todos os serviços definidos no seu `docker-compose.yml`. Use `-d` para rodar em background (modo *detached*). |
| **`docker-compose down`** | **Parar os serviços:** Para e remove os containers, redes e (opcionalmente) volumes criados pelo `up`. |
| **`docker-compose restart`**| **Reiniciar os serviços:** Reinicia todos os serviços do seu projeto. |
| **`docker-compose ps`** | **Listar serviços:** Mostra o status dos containers gerenciados pelo Compose. |

---

### 🌐 Redes & Conexões
Containers precisam se comunicar!

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`docker network create`** | **Criar uma rede:** Cria uma rede virtual para que seus containers possam se comunicar pelo nome, de forma isolada. | `docker network create --driver bridge minha-rede` |
| **`docker network ls`** | **Listar redes:** Exibe todas as redes Docker disponíveis. | `docker network ls` |
| **`hostname -i`** | **Ver o IP do container:** **Dentro do container**, este comando Linux mostra o IP interno dele na rede Docker. | `hostname -i` |

---

### ✨ Dicas de Ouro e Limpeza
Mantenha seu ambiente Docker limpo e organizado!

| Comando | O que faz? |
| :--- | :--- |
| **`docker system prune -a`** | **Faxina Geral!** **CUIDADO!** Remove todos os containers parados, redes não utilizadas, o cache de build e **todas** as imagens que não estão em uso. |
| **`docker container prune`** | **Limpar containers inativos:** Remove apenas os containers que estão parados. Uma forma mais segura de limpar o básico. |
| **`docker ps -q`** | **Listar apenas os IDs:** Retorna somente o ID dos containers ativos. Perfeito para usar em scripts, como no comando `docker stop $(docker ps -q)`. |# 🐳 Guia de Comandos Docker: Do Básico ao Avançado! 🚀

Olá, marinheiro de primeira viagem (ou capitão experiente)! Navegar no oceano do Docker pode ser desafiador, mas com os comandos certos, você se tornará um mestre dos containers.

Este guia foi atualizado para ser mais didático e visual, te ajudando a encontrar o que precisa rapidamente. Vamos zarpar!

---

### 🚢 Gerenciando Containers (O Coração do Docker)
Aqui estão os comandos para interagir com seus containers no dia a dia.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`docker ps`** | **Listar containers ativos:** Mostra apenas os containers que estão em execução no momento. | `docker ps` |
| **`docker ps -a`** | **Listar TODOS os containers:** Exibe todos os containers, incluindo os que estão parados. Super útil para limpeza! | `docker ps -a` |
| **`docker start`** | **Iniciar um container:** "Acorda" um container que estava parado. | `docker start <ID_OU_NOME_DO_CONTAINER>` |
| **`docker stop`** | **Parar um container:** Envia um sinal para parar a execução de um container de forma segura. | `docker stop <ID_OU_NOME_DO_CONTAINER>` |
| **`docker stop $(docker ps -q)`** | **Parar TODOS os containers:** Um comando poderoso para parar todos os containers em execução de uma só vez. | `docker stop $(docker ps -q)` |
| **`docker rm`** | **Remover um container:** Apaga um container que **não está em execução**. Para forçar a remoção de um em execução, use a flag `-f`. | `docker rm <ID_OU_NOME_DO_CONTAINER>` |
| **`docker inspect`** | **Inspecionar um container:** Fornece um mar de informações detalhadas sobre o container em formato JSON (redes, volumes, etc). | `docker inspect <ID_OU_NOME_DO_CONTAINER>` |
| **`docker exec -it`** | **Entrar em um container:** A forma **mais recomendada** de abrir um terminal interativo (`-it`) dentro de um container que já está rodando. | `docker exec -it <ID_OU_NOME> /bin/bash` |
| **`docker attach`** | **Anexar a um container:** Conecta seu terminal ao processo principal do container. **Cuidado:** se você sair com `Ctrl+C`, o container pode parar! | `docker attach <ID_OU_NOME_DO_CONTAINER>` |
| **`docker port`** | **Verificar portas mapeadas:** Mostra como as portas do container estão mapeadas para as portas da sua máquina. | `docker port <ID_OU_NOME_DO_CONTAINER>` |
| **`docker cp`** | **Copiar arquivos:** Copia arquivos e pastas entre sua máquina e o container (nos dois sentidos!). | `docker cp arquivo.txt meu_container:/app/` |

---

### 🖼️ Gerenciando Imagens (Os Moldes dos Seus Containers)
Imagens são os blueprints. Veja como gerenciá-las.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`docker pull`** | **Baixar uma imagem:** Faz o download de uma imagem do Docker Hub (ou outro registro). | `docker pull ubuntu:latest` |
| **`docker images`** | **Listar imagens locais:** Mostra todas as imagens que você já baixou para a sua máquina. | `docker images` |
| **`docker build -t`** | **Construir uma imagem:** Cria uma nova imagem a partir de um `Dockerfile`. O `-t` define o nome e a tag (`<nome>:<versao>`). | `docker build -t minha-app:1.0 .` |
| **`docker tag`** | **Criar tag para uma imagem:** Aplica um novo "rótulo" a uma imagem existente. Essencial para versionar e enviar ao registro. | `docker tag <ID_DA_IMAGEM> meu-usuario/minha-app:1.0` |
| **`docker push`** | **Enviar imagem para o Hub:** Publica sua imagem em um registro como o Docker Hub para compartilhar com o mundo. | `docker push meu-usuario/minha-app:1.0` |
| **`docker rmi`** | **Remover uma imagem:** Apaga uma imagem da sua máquina. A imagem não pode estar sendo usada por nenhum container. | `docker rmi <ID_DA_IMAGEM>` |
| **`docker commit`** | **Criar imagem de um container:** Salva o estado atual de um container como uma nova imagem. Útil para debug, mas o ideal é sempre usar um Dockerfile. | `docker commit <ID_DO_CONTAINER> nova-imagem:debug` |
| **`docker save`** | **Salvar imagem em um arquivo:** Exporta sua imagem para um arquivo `.tar`, facilitando o backup ou a transferência manual. | `docker save minha-app:1.0 > minha-app.tar` |
| **`docker load`** | **Carregar imagem de um arquivo:** Importa uma imagem a partir de um arquivo `.tar`. | `docker load < minha-app.tar` |

---

### 🎼 Docker Compose (Orquestrando Múltiplos Containers)
Para projetos com vários serviços (ex: app + banco de dados), o `docker-compose` é seu melhor amigo.

| Comando | O que faz? |
| :--- | :--- |
| **`docker-compose up`** | **Iniciar os serviços:** Sobe todos os serviços definidos no seu `docker-compose.yml`. Use `-d` para rodar em background (modo *detached*). |
| **`docker-compose down`** | **Parar os serviços:** Para e remove os containers, redes e (opcionalmente) volumes criados pelo `up`. |
| **`docker-compose restart`**| **Reiniciar os serviços:** Reinicia todos os serviços do seu projeto. |
| **`docker-compose ps`** | **Listar serviços:** Mostra o status dos containers gerenciados pelo Compose. |

---

### 🌐 Redes & Conexões
Containers precisam se comunicar!

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`docker network create`** | **Criar uma rede:** Cria uma rede virtual para que seus containers possam se comunicar pelo nome, de forma isolada. | `docker network create --driver bridge minha-rede` |
| **`docker network ls`** | **Listar redes:** Exibe todas as redes Docker disponíveis. | `docker network ls` |
| **`hostname -i`** | **Ver o IP do container:** **Dentro do container**, este comando Linux mostra o IP interno dele na rede Docker. | `hostname -i` |

---

### ✨ Dicas de Ouro e Limpeza
Mantenha seu ambiente Docker limpo e organizado!

| Comando | O que faz? |
| :--- | :--- |
| **`docker system prune -a`** | **Faxina Geral!** **CUIDADO!** Remove todos os containers parados, redes não utilizadas, o cache de build e **todas** as imagens que não estão em uso. |
| **`docker container prune`** | **Limpar containers inativos:** Remove apenas os containers que estão parados. Uma forma mais segura de limpar o básico. |
| **`docker ps -q`** | **Listar apenas os IDs:** Retorna somente o ID dos containers ativos. Perfeito para usar em scripts, como no comando `docker stop $(docker ps -q)`. |