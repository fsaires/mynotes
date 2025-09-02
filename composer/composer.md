# 🐘 Guia de Comandos PHP Composer: Seu Gerenciador de Dependências!

Composer é o maestro da orquestra do seu projeto PHP! Ele gerencia todas as bibliotecas (pacotes) que seu projeto precisa, resolve conflitos e garante que tudo funcione em harmonia.

Este guia rápido vai te ajudar a dominar os comandos mais importantes.

---

### 💡 Uma Nota Rápida Sobre a Instalação

Nos exemplos, usaremos o comando `composer` diretamente. Isso funciona quando o Composer está instalado globalmente e adicionado ao PATH do seu sistema, o que é a prática mais comum. Se você o executa de outra forma (como `php composer.phar`), basta substituir `composer` pelo seu comando.

---

### 🚀 Começando um Projeto

Do zero a um projeto funcional em segundos!

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`create-project`** | **Criar um novo projeto:** Inicia um novo projeto a partir de um esqueleto existente, como Laravel ou Symfony, já baixando todas as suas dependências. | `composer create-project --prefer-dist laravel/laravel nome-do-projeto` |

---

### 📦 Gerenciando Dependências no Dia a Dia

Adicione, atualize e remova os pacotes que dão superpoderes ao seu código.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`require`** | **Adicionar um pacote:** Adiciona uma nova dependência ao seu `composer.json` e a instala. Use `--dev` para pacotes de desenvolvimento (testes, debug, etc.). | `composer require monolog/monolog` |
| **`install`** | **Instalar dependências:** Lê o arquivo `composer.lock` e instala as versões exatas das dependências listadas lá. **É o comando que você deve usar para instalar um projeto existente!** | `composer install` |
| **`update`** | **Atualizar dependências:** Verifica o `composer.json`, busca as versões mais recentes permitidas para seus pacotes e atualiza o `composer.lock`. | `composer update` |
| **`remove`** | **Remover um pacote:** Remove uma dependência do seu projeto e atualiza os arquivos `composer.json` e `composer.lock`. | `composer remove monolog/monolog` |

> **Dica de Ouro:** `install` vs `update`
> * `composer install`: Usa o `composer.lock` para garantir que todos na equipe usem as **mesmas versões** dos pacotes. É rápido e seguro.
> * `composer update`: Atualiza os pacotes para novas versões e **recria** o `composer.lock`. Use com cuidado para evitar quebrar o projeto.

---

### 🔍 Diagnóstico e Informações

Comandos para entender e depurar seu ambiente.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`diagnose`** | **Verificar status:** Executa uma série de verificações para diagnosticar problemas comuns na sua configuração do Composer. | `composer diagnose` |
| **`show`** | **Listar pacotes:** Mostra todos os pacotes que estão instalados no projeto, incluindo suas versões e descrições. | `composer show` |
| **`search`** | **Buscar pacotes:** Procura por pacotes disponíveis no Packagist (o repositório principal do Composer). | `composer search monolog` |

---

### ✨ Dicas de Performance para Produção

Deixe seu projeto voando em produção!

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`install --no-dev`** | **Instalação para produção:** Instala apenas as dependências de produção, ignorando os pacotes de desenvolvimento. | `composer install --no-dev --optimize-autoloader` |
| **`dump-autoload -o`** | **Otimizar o autoloader:** Gera um mapa de classes super otimizado (`-o`), tornando o carregamento de arquivos muito mais rápido. **Sempre execute isso no deploy!** | `composer dump-autoload -o` |