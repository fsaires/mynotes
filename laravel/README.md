# 🐘 Guia de Comandos Laravel Artisan: Seu Canivete Suíço

`artisan` é a interface de linha de comando incluída no Laravel. Ele fornece um número impressionante de comandos úteis que podem te ajudar a construir sua aplicação rapidamente. Pense nele como o seu assistente pessoal para o desenvolvimento em Laravel.

Este guia reúne os comandos mais importantes para o seu dia a dia.

---

### 🚀 Iniciando e Configurando um Projeto

Os primeiros passos após criar um novo projeto Laravel.

| Comando | O que faz? |
| :--- | :--- |
| **`composer create-project`** | **Criar um novo projeto:** Baixa e instala uma nova aplicação Laravel. |
| **`php artisan key:generate`** | **Gerar a chave da aplicação:** Define a `APP_KEY` no seu arquivo `.env`. **É o primeiro comando que você deve rodar** após a instalação. |
| **`php artisan serve`** | **Iniciar o servidor local:** Sobe um servidor de desenvolvimento em `http://127.0.0.1:8000`. |
| **`php artisan down`** | **Ativar o modo de manutenção:** Coloca sua aplicação em modo de manutenção, exibindo uma página de erro 503 para todos os visitantes. |
| **`php artisan up`** | **Desativar o modo de manutenção:** Tira a aplicação do modo de manutenção. |

**Exemplo de Uso:**
```bash
composer create-project --prefer-dist laravel/laravel meu-blog
cd meu-blog
php artisan key:generate
```

---

### 🗃️ Banco de Dados: Migrations e Seeders

Gerencie a estrutura e os dados iniciais do seu banco de dados com facilidade.

| Comando | O que faz? |
| :--- | :--- |
| **`php artisan migrate`** | **Executar as migrations:** Cria no banco de dados todas as tabelas definidas nos seus arquivos de migration que ainda não foram executadas. |
| **`php artisan migrate:fresh`** | **Recriar o banco de dados:** **CUIDADO!** Apaga todas as tabelas e executa novamente todas as migrations. Muito útil em ambiente de desenvolvimento. |
| **`php artisan migrate:rollback`**| **Desfazer a última migration:** Reverte o último "lote" de migrations que foi executado. |
| **`php artisan make:seeder`** | **Criar um Seeder:** Gera um novo arquivo de seeder para popular tabelas com dados iniciais ou de teste. |
| **`php artisan db:seed`** | **Executar os Seeders:** Roda a classe `DatabaseSeeder` (e as outras que ela chamar) para popular o banco de dados. |

**Exemplo de Uso:**
```bash
# Para recriar o banco e popular com dados de teste de uma só vez
php artisan migrate:fresh --seed
```

---

### 🏗️ Gerando Código (Comandos `make`)

Acelere seu desenvolvimento gerando automaticamente os arquivos básicos para Models, Controllers e muito mais.

| Comando | O que faz? |
| :--- | :--- |
| **`php artisan make:model`** | **Criar um Model:** Gera uma nova classe de Model. Use flags para criar arquivos relacionados ao mesmo tempo. |
| **`php artisan make:controller`**| **Criar um Controller:** Gera uma nova classe de Controller. |
| **`php artisan make:migration`**| **Criar uma Migration:** Gera um novo arquivo de migration para criar ou alterar uma tabela. |
| **`php artisan make:factory`** | **Criar uma Factory:** Gera uma factory para facilitar a criação de models com dados falsos para testes ou seeders. |

**Exemplos de Uso (com flags mágicas ✨):**
```bash
# Cria um Model, uma Migration (-m), um Controller de recurso (-cr) e uma Factory (-f) de uma só vez!
php artisan make:model Post -mcrf

# Cria um Controller de recurso (com métodos index, create, store, show, edit, update, destroy)
php artisan make:controller PhotoController --resource
```

---

### 🛠️ Comandos Úteis do Dia a Dia

Ferramentas para inspecionar, depurar e otimizar sua aplicação.

| Comando | O que faz? |
| :--- | :--- |
| **`php artisan route:list`** | **Listar todas as rotas:** Mostra uma tabela com todas as rotas registradas na sua aplicação. |
| **`php artisan tinker`** | **Abrir um console interativo:** Inicia um REPL (Read-Eval-Print Loop) para você interagir com sua aplicação Laravel diretamente pelo terminal. |
| **`php artisan config:cache`** | **Otimizar configuração:** Cria um único arquivo de cache com todas as configurações, acelerando a aplicação. **Use em produção!** |
| **`php artisan route:cache`** | **Otimizar rotas:** Cria um arquivo de cache de rotas. **Use em produção!** |
| **`php artisan backup:run`** | **Executar backup:** Inicia um backup da aplicação. (Requer o pacote `spatie/laravel-backup`). |

**Exemplo de Uso:**
```bash
# Fazer backup apenas do banco de dados
php artisan backup:run --only-db
```