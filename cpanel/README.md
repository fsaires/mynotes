# 🌐 Guia para Hospedagem Compartilhada (cPanel): Dicas para Desenvolvedores

Hospedagem compartilhada é a porta de entrada para muitos projetos na web. É uma solução de baixo custo onde vários sites dividem os recursos de um único servidor, gerenciado através de um painel de controle como o **cPanel**.

Apesar de suas limitações, é possível trabalhar com ferramentas modernas como Git, Composer e frameworks como Laravel. Este guia foca em dicas e truques para aproveitar ao máximo esse ambiente.

---

### 🎛️ Dominando as Ferramentas Essenciais do cPanel

O cPanel é o seu centro de comando. Conhecer as ferramentas certas economiza muito tempo.

| Ferramenta | O que faz? | Dica de Uso |
| :--- | :--- | :--- |
| **Gerenciador de Arquivos** | Permite enviar, baixar e editar arquivos diretamente pelo navegador. | Ótimo para edições rápidas ou para descompactar um arquivo `.zip` que você enviou. |
| **Contas de FTP** | Cria e gerencia usuários para acesso via FTP (ex: com FileZilla). | Use para transferir grandes quantidades de arquivos de forma mais confiável que o gerenciador web. |
| **Bancos de Dados MySQL®**| Cria novos bancos de dados e usuários para eles. | Sempre crie um usuário específico para cada banco de dados. Anote a senha! |
| **phpMyAdmin** | Interface gráfica para gerenciar o conteúdo do seu banco de dados. | Essencial para importar/exportar bancos (`.sql`) e executar queries manuais. |
| **MultiPHP Manager** | Permite alterar a versão do PHP para cada um dos seus domínios. | Verifique se seu projeto está rodando na versão do PHP recomendada pelo framework que você usa. |
| **MultiPHP INI Editor** | Permite editar configurações do PHP (`php.ini`), como `memory_limit` e `upload_max_filesize`. | Aumente os limites se estiver recebendo erros de memória ou ao tentar enviar arquivos grandes. |
| **Acesso SSH** | Libera o acesso ao terminal do servidor. **A ferramenta mais importante para desenvolvedores.** | Se não estiver habilitado, procure por esta opção no seu painel ou peça ao suporte para liberar. |
| **Cron Jobs (Tarefas Cron)**| Permite agendar a execução de comandos em intervalos de tempo específicos. | Indispensável para automatizar rotinas, como o agendador de tarefas do Laravel. |

---

### 🚀 Dicas Avançadas para o Terminal (SSH)

Uma vez conectado via SSH, você ganha superpoderes. Mas ambientes compartilhados têm suas peculiaridades.

#### Executando o Composer (O Grande Desafio)

A limitação de memória é o principal inimigo do Composer em hospedagens compartilhadas. A solução é executar o comando do PHP passando um novo limite de memória na própria chamada.

1.  **Instale o Composer:** Primeiro, baixe o `composer.phar` para o seu diretório home:
    ```bash
    # Conecte-se via SSH e rode:
    php -r "copy('[https://getcomposer.org/installer](https://getcomposer.org/installer)', 'composer-setup.php');"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    # Agora você terá o arquivo 'composer.phar' no seu diretório
    ```

2.  **Execute os comandos do Composer sem limite de memória:**
    * **O comando mágico:**
        ```bash
        php -d memory_limit=-1 composer.phar install
        ```
    * **Anatomia do Comando:**
        * `php -d memory_limit=-1`: Executa o PHP **apenas para este comando** com o limite de memória (`memory_limit`) definido como ilimitado (`-1`). Isso "engana" a restrição do servidor.
        * `composer.phar`: É o arquivo do Composer que você baixou. Você precisa especificar o caminho até ele.
        * `install` / `update` / `require`: O comando do Composer que você deseja executar.

#### Agendando Tarefas (Cron Job) com Laravel

Para fazer o `php artisan schedule:run` do Laravel funcionar, você precisa configurar um Cron Job no cPanel com o seguinte comando:

```bash
# O comando a ser inserido no cPanel Cron Jobs
* * * * * cd /home/seu_usuario/public_html/seu_projeto && /usr/local/bin/php artisan schedule:run >> /dev/null 2>&1
```

* **Anatomia do Comando:**
    * `* * * * *`: Executa o comando a cada minuto.
    * `cd /home/...`: **Essencial!** Navega para a pasta do seu projeto primeiro.
    * `/usr/local/bin/php`: Use o caminho completo para o executável do PHP para garantir que a versão correta seja usada.
    * `>> /dev/null 2>&1`: Impede que a tarefa cron envie e-mails de notificação a cada execução.