# 🐘 Guia de Comandos MySQL: Manutenção e Boas Práticas

Manter um banco de dados saudável vai além de criar tabelas e inserir dados. É crucial garantir que ele utilize os padrões corretos de `character set` para suportar todos os tipos de caracteres (como emojis 😉 e acentos) e o `storage engine` adequado para garantir a integridade dos seus dados.

Este guia foca nesses comandos essenciais de manutenção e diagnóstico.

---

### ⚙️ Gerenciando Character Sets e Collations (UTF-8 & utf8mb4)

Garantir que seu banco de dados "fale a língua" da internet moderna é fundamental. O padrão `utf8mb4` é a escolha certa para suportar um range completo de caracteres Unicode.

| Comando/Query | O que faz? |
| :--- | :--- |
| **`ALTER DATABASE`** | **Define o padrão do banco:** Altera o conjunto de caracteres e a `collation` padrão para **novas tabelas** que forem criadas no banco de dados. |
| **`ALTER TABLE`** | **Converte uma tabela:** Altera o conjunto de caracteres e a `collation` de uma tabela **existente** e de todas as suas colunas de texto. |
| **`ALTER TABLE ... MODIFY`** | **Converte uma coluna específica:** Altera o `character set` e a `collation` de uma única coluna. |

**Exemplos de Uso:**

* **Definir o padrão para um banco de dados inteiro:**
    ```sql
    ALTER DATABASE nome_do_banco DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ```

* **Converter uma tabela e todas as suas colunas para `utf8mb4`:**
    ```sql
    ALTER TABLE nome_da_tabela CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ```

* **Modificar apenas uma coluna:**
    ```sql
    ALTER TABLE nome_da_tabela MODIFY nome_da_coluna VARCHAR(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ```

> **Dica de Ouro:** `utf8` vs `utf8mb4`
> O `utf8` no MySQL é um apelido para `utf8mb3` e não suporta caracteres de 4 bytes, como a maioria dos emojis. **Sempre prefira `utf8mb4`** em novos projetos para máxima compatibilidade.

---

### 🔩 Gerenciando Storage Engines (InnoDB vs. MyISAM)

O `storage engine` define como o MySQL armazena e gerencia os dados de uma tabela. `InnoDB` é o padrão e o mais recomendado na maioria dos casos.

| Comando/Query | O que faz? |
| :--- | :--- |
| **`ALTER TABLE ... ENGINE`** | **Mudar o Storage Engine:** Converte o motor de armazenamento de uma tabela. A conversão de `MyISAM` para `InnoDB` é muito comum. |

**Exemplo de Uso:**

* **Converter uma tabela de MyISAM para InnoDB:**
    ```sql
    ALTER TABLE nome_da_tabela ENGINE = InnoDB;
    ```

> **Por que usar InnoDB?**
> `InnoDB` oferece suporte a transações (ACID), chaves estrangeiras (`foreign keys`) e recuperação de falhas, funcionalidades essenciais para a maioria das aplicações modernas. `MyISAM` é mais antigo e não possui esses recursos.

---

### 🔍 Consultas de Diagnóstico
Antes de alterar, inspecione! Use estas queries na `information_schema` para entender o estado atual do seu banco.

* **Encontrar todas as tabelas que ainda usam `MyISAM`:**
    ```sql
    SELECT TABLE_NAME, ENGINE 
    FROM information_schema.TABLES
    WHERE TABLE_SCHEMA = 'nome_do_banco' AND ENGINE = 'MyISAM';
    ```

* **Encontrar todas as colunas que não usam uma `collation` específica (ex: para migrar de `utf8` para `utf8mb4`):**
    ```sql
    SELECT TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLLATION_NAME
    FROM information_schema.columns 
    WHERE COLLATION_NAME != 'utf8mb4_unicode_ci' 
      AND TABLE_SCHEMA = 'nome_do_banco'
      -- Exclui os bancos de dados internos do MySQL da busca
      AND TABLE_SCHEMA NOT IN ('information_schema','mysql', 'performance_schema','sys');
    ```