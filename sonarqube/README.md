# SonarQube: Análise de Qualidade de Código com Docker

SonarQube é a plataforma líder para inspeção contínua da qualidade do código. Ela realiza análises estáticas para detectar bugs, "code smells" (maus cheiros no código) e vulnerabilidades de segurança.

Usar Docker é uma forma excelente e rápida de rodar tanto o servidor do SonarQube quanto o scanner para analisar seus projetos.

---

### 🏡 Passo 1: Rodar o Servidor SonarQube Localmente

Antes de analisar, você precisa de uma instância do SonarQube para receber os relatórios.

1.  **Crie uma rede Docker:** Para que o scanner possa se comunicar com o servidor, ambos precisam estar na mesma rede.
    ```bash
    docker network create sonar-net
    ```

2.  **Inicie o container do SonarQube:**
    ```bash
    docker run -d --name sonarqube -p 9000:9000 --network sonar-net sonarsource/sonarqube-community:latest
    ```
    * `--name sonarqube`: Dá um nome fácil ao container.
    * `-p 9000:9000`: Mapeia a porta do container para a sua máquina.
    * `--network sonar-net`: Conecta o container à rede que criamos.

3.  **Acesse a interface:** Aguarde um ou dois minutos para o servidor iniciar e acesse **`http://localhost:9000`** no seu navegador. As credenciais iniciais são `admin` / `admin`. Você será solicitado a trocar a senha no primeiro login.

---

### 🔍 Passo 2: Preparar e Executar a Análise

Com o servidor rodando, agora vamos preparar e analisar seu projeto.

1.  **Gere um Token de Acesso:** O scanner precisa de um token para se autenticar.
    * Na interface do SonarQube, vá em **Minha Conta > Segurança**.
    * Gere um novo token e **copie o valor gerado**.

2.  **Crie o arquivo de configuração:** Na raiz do seu projeto, crie um arquivo chamado `sonar-project.properties` com o seguinte conteúdo:
    ```properties
    # Chave única para o seu projeto
    sonar.projectKey=meu-projeto-chave

    # Nome do projeto que aparecerá no dashboard
    sonar.projectName=Meu Projeto Incrível
    
    # Versão do projeto
    sonar.projectVersion=1.0

    # Caminho para o código fonte ('.' significa o diretório atual)
    sonar.sources=.

    # Encoding do seu código fonte
    sonar.sourceEncoding=UTF-8
    ```

3.  **Execute o Scanner via Docker:** Navegue até a pasta raiz do seu projeto pelo terminal e rode o comando abaixo.

    * **O Comando:**
        ```bash
        docker run \
            -e SONAR_HOST_URL=http://sonarqube:9000 \
            -e SONAR_TOKEN="COLE_SEU_TOKEN_AQUI" \
            -v "${PWD}:/usr/src" \
            --network sonar-net \
            --rm \
            sonarsource/sonar-scanner-cli
        ```
    * **Anatomia do Comando:**

| Parâmetro | O que faz? |
| :--- | :--- |
| **`-e SONAR_HOST_URL`** | Aponta para o container do servidor na rede Docker (`http://sonarqube:9000`). |
| **`-e SONAR_TOKEN`** | Passa o token de autenticação que você gerou. |
| **`-v "${PWD}:/usr/src"`** | **A parte mais importante!** Mapeia o seu diretório de projeto atual (`${PWD}`) para o diretório `/usr/src` dentro do container do scanner, permitindo que ele leia seu código. |
| **`--network sonar-net`** | Conecta o container do scanner à mesma rede do servidor. |
| **`--rm`** | Remove o container do scanner automaticamente após a conclusão da análise. |
| **`sonarsource/sonar-scanner-cli`** | A imagem Docker do scanner oficial. |

> **Nota para usuários de Windows (CMD):** Troque `${PWD}` por `%CD%` no comando acima.

---

### ✨ Passo 3: Visualizar os Resultados

Após o comando do scanner terminar com a mensagem `EXECUTION SUCCESS`, volte para a interface do SonarQube em **`http://localhost:9000`**. Seu projeto aparecerá no dashboard com o relatório completo da análise de qualidade!