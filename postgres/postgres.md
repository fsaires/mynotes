# 🐘 Guia de Comandos PostgreSQL: Do Servidor ao SQL

PostgreSQL é um dos bancos de dados relacionais open-source mais poderosos e confiáveis do mundo. Dominar seus comandos, tanto para gerenciar o servidor quanto para interagir com os dados via `psql`, é essencial para qualquer desenvolvedor.

Este guia reúne os comandos mais importantes de forma organizada e didática.

---

### 🔧 Gerenciando o Servidor (Via Linha de Comando)

Estes comandos, usando `pg_ctl`, são para controle manual do serviço do PostgreSQL.

| Comando | O que faz? | Exemplo de Uso (genérico) |
| :--- | :--- | :--- |
| **`pg_ctl start`** | **Iniciar o servidor:** Liga o serviço do banco de dados, apontando para o diretório de dados (`-D`). | `pg_ctl -D /caminho/para/data start` |
| **`pg_ctl stop`** | **Parar o servidor:** Desliga o serviço de forma segura. | `pg_ctl -D /caminho/para/data stop` |
| **`pg_ctl restart`**| **Reiniciar o servidor:** Para e inicia o serviço novamente. Útil para aplicar certas configurações. | `pg_ctl -D /caminho/para/data restart` |
| **`pg_ctl status`**| **Verificar o status:** Mostra se o servidor PostgreSQL está em execução. | `pg_ctl -D /caminho/para/data status` |

> **Dica de Ouro:** Na maioria dos sistemas (Windows, Linux, macOS), o PostgreSQL é configurado para rodar como um **serviço** (`service` ou `systemctl`), que inicia automaticamente com o sistema. O uso de `pg_ctl` é mais comum para troubleshooting ou gerenciamento de múltiplas instâncias manuais.

---

### 🚀 Conectando e Navegando com `psql`

`psql` é o terminal interativo do PostgreSQL. É aqui que a mágica acontece!

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`psql -U <user>`** | **Conectar ao banco:** A forma mais comum de se conectar, especificando o usuário (`-U`), o banco (`-d`) e o host (`-h`). | `psql -U postgres -d meu_banco -h localhost` |
| **`\l` ou `\l+`**| **Listar bancos de dados:** Mostra todos os bancos de dados disponíveis no servidor. A versão com `+` dá mais detalhes. | `\l` |
| **`\c <database>`** | **Conectar a um banco:** Troca a sua conexão atual para outro banco de dados. | `\c nome_do_banco` |
| **`\conninfo`** | **Ver info da conexão:** Mostra informações sobre a sua conexão atual (usuário, banco, host, porta). | `\conninfo` |
| **`\q`** | **Sair do psql:** Desconecta e fecha o terminal interativo. | `\q` |

---

### 🔍 Inspecionando o Banco de Dados (Meta-comandos `psql`)

Depois de conectado, use estes "atalhos" para explorar a estrutura do seu banco.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`\dt`** | **Listar tabelas:** Mostra as tabelas do schema atual (geralmente `public`). | `\dt` |
| **`\d <tabela>`** | **Descrever uma tabela:** Exibe as colunas, tipos de dados, índices e constraints de uma tabela. **Muito útil!** | `\d usuarios` |
| **`\dn`** | **Listar schemas:** Mostra os schemas do banco de dados. | `\dn` |
| **`\df`** | **Listar funções:** Mostra as funções disponíveis. | `\df` |
| **`\dv`** | **Listar views:** Mostra as views disponíveis. | `\dv` |
| **`\du`** | **Listar usuários (roles):** Exibe todos os usuários e suas permissões. | `\du` |
| **`\timing`** | **Ativar cronômetro:** Mostra o tempo de execução de cada query que você rodar. | `\timing` |

---

### 🔩 Comandos SQL Úteis

Queries SQL padrão que são frequentemente usadas para tarefas administrativas.

* **Exibir o encoding do servidor:**
    ```sql
    SHOW SERVER_ENCODING;
    ```

* **Exibir o encoding do cliente:**
    ```sql
    SHOW CLIENT_ENCODING;
    ```

* **Reiniciar o valor de uma `SEQUENCE`:**
    ```sql
    -- Faz com que o próximo valor da sequence seja 1
    ALTER SEQUENCE nome_da_sequence RESTART WITH 1;
    ```

* **Criar um novo banco de dados:**
    ```sql
    CREATE DATABASE meu_novo_banco WITH OWNER meu_usuario ENCODING 'UTF8';
    ```

* **Criar um novo usuário (role) com senha:**
    ```sql
    CREATE ROLE novo_usuario WITH LOGIN PASSWORD 'senha_forte';
    ```

* **Conceder todos os privilégios de um banco a um usuário:**
    ```sql
    GRANT ALL PRIVILEGES ON DATABASE meu_banco TO novo_usuario;
    ```