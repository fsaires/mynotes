# 🐘 Guia WordPress: Dicas para Desenvolvimento Local e Migração

Trabalhar com o WordPress em um ambiente local é uma prática essencial para desenvolver e testar com segurança. Um dos maiores desafios é migrar um site de um servidor online para a sua máquina (e vice-versa), o que quase sempre envolve a correção de URLs.

Este guia reúne os comandos e passos cruciais para fazer essa transição de forma tranquila.

---

### 📄 O Coração do Site: O Arquivo `wp-config.php`

Antes de qualquer coisa, ao mover um site WordPress, seu primeiro passo deve ser conferir o arquivo `wp-config.php`. Ele contém as configurações mais críticas.

| Constante | O que faz? | Exemplo de Configuração Local |
| :--- | :--- | :--- |
| **`DB_NAME`** | **Nome do Banco de Dados:** O nome do banco de dados que o WordPress usará. | `define( 'DB_NAME', 'meu_banco_local' );` |
| **`DB_USER`** | **Usuário do Banco:** O usuário para se conectar ao banco. | `define( 'DB_USER', 'root' );` |
| **`DB_PASSWORD`** | **Senha do Banco:** A senha para o usuário do banco. | `define( 'DB_PASSWORD', 'root' );` |
| **`DB_HOST`** | **Host do Banco:** O endereço do servidor de banco de dados. | `define( 'DB_HOST', 'localhost' );` |
| **`WP_DEBUG`** | **Modo de Debug:** **Essencial para dev!** Ativa a exibição de erros e alertas do PHP no site. | `define( 'WP_DEBUG', true );` |

---

### 🔗 Corrigindo URLs no Banco de Dados

Depois de migrar o banco de dados, você precisa dizer ao WordPress qual é o seu novo "endereço" local.

#### Método 1: SQL Direto (O seu comando)
Este método é rápido para corrigir as URLs principais, mas pode não atualizar links dentro do conteúdo das páginas.

* **Comando:**
    ```sql
    UPDATE wp_options SET option_value = 'http://localhost/meu-site' WHERE option_name IN ('home', 'siteurl');
    ```
* **O que faz?**
    Atualiza as duas opções mais importantes que definem o endereço do seu site no WordPress.
* ⚠️ **Atenção:** Se o prefixo das suas tabelas não for `wp_`, lembre-se de alterá-lo na query (ex: `UPDATE meu_prefixo_options ...`).

#### Método 2: Usando WP-CLI (Recomendado)
WP-CLI é a interface de linha de comando oficial do WordPress. É a forma mais segura e completa de fazer a busca e substituição de URLs, pois lida corretamente com dados serializados.

* **Comando:**
    ```bash
    wp search-replace '[https://www.site-online.com](https://www.site-online.com)' 'http://localhost/meu-site' --all-tables
    ```
* **O que faz?**
    Procura em **todas as tabelas** do banco de dados pela URL antiga e a substitui pela nova, sem corromper dados.

#### Método 3: Usando Plugins
Para quem prefere uma interface gráfica, plugins como o **Better Search Replace** permitem fazer essa substituição de forma segura diretamente do painel do WordPress.

---

### 🔄 Passo Final: Regenerar os Permalinks
Após mudar as URLs, é muito comum que as páginas internas (além da home) retornem um erro 404. A solução é simples:

1.  Acesse o painel do WordPress.
2.  Vá para **Configurações > Links Permanentes**.
3.  **Não altere nada!** Apenas clique no botão **"Salvar alterações"**.

Isso fará com que o WordPress regenere o arquivo `.htaccess` com as novas regras de reescrita de URL, corrigindo os erros 404.
