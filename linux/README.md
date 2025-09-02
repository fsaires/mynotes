# 🐧 Guia de Comandos Linux: O Essencial para Desenvolvedores

O terminal do Linux é uma das ferramentas mais poderosas à disposição de um desenvolvedor. Dominar seus comandos essenciais aumenta drasticamente a produtividade e o controle sobre o ambiente de desenvolvimento e produção.

Este guia reúne comandos fundamentais, organizados por categoria, para você ter sempre à mão.

---

### 📂 Navegação e Gerenciamento de Arquivos
Os comandos básicos para se mover pelo sistema de arquivos e manipular diretórios e arquivos.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`ls -la`** | **Listar arquivos:** Mostra todos os arquivos e diretórios (`-a`), em formato de lista longa (`-l`), com detalhes como permissões e tamanho. | `ls -la /var/www` |
| **`cd`** | **Mudar de diretório:** Navega para o diretório especificado. `cd ..` sobe um nível. | `cd /home/usuario/projetos` |
| **`pwd`** | **Mostrar diretório atual:** Imprime o caminho completo do diretório onde você está. | `pwd` |
| **`mkdir`** | **Criar diretório:** Cria um novo diretório. Use a flag `-p` para criar diretórios aninhados. | `mkdir -p meus_docs/fotos` |
| **`cp`** | **Copiar:** Copia arquivos ou diretórios. Use a flag `-r` para copiar diretórios recursivamente. | `cp arquivo.txt backup.txt` |
| **`mv`** | **Mover ou Renomear:** Move um arquivo para outro local ou simplesmente o renomeia. | `mv antigo.txt novo.txt` |
| **`rm`** | **Remover:** Apaga arquivos. Use `-r` para diretórios e `-f` para forçar a remoção. **Use com extremo cuidado!** | `rm arquivo_temporario.log` |
| **`cat` / `less`** | **Ver conteúdo:** `cat` exibe o conteúdo de um arquivo de uma vez. `less` exibe de forma paginada (use 'q' para sair). | `cat .env` ou `less error.log` |

---

### ⚙️ Gerenciamento de Serviços e Processos
Controle os serviços (como Apache, Nginx, MySQL) e monitore os processos do seu sistema.

| Comando | O que faz? |
| :--- | :--- |
| **`systemctl start`** | **Iniciar um serviço:** Inicia um serviço gerenciado pelo `systemd` (o padrão moderno). |
| **`systemctl stop`** | **Parar um serviço:** Para a execução de um serviço. |
| **`systemctl restart`** | **Reiniciar um serviço:** Para e inicia o serviço novamente. É o equivalente moderno do `service apache2 restart`. |
| **`systemctl status`** | **Verificar o status:** Mostra informações detalhadas sobre um serviço, incluindo se está ativo e os últimos logs. |
| **`systemctl enable`** | **Habilitar na inicialização:** Configura um serviço para iniciar automaticamente com o boot do sistema. |
| **`ps aux`** | **Listar processos:** Mostra todos os processos em execução no sistema. |
| **`htop`** | **Monitorar processos:** Abre um monitor interativo de processos, uso de CPU e memória. (Pode precisar ser instalado: `sudo apt install htop`). |
| **`kill`** | **Matar um processo:** Encerra um processo usando seu ID (PID). |

**Exemplo de Uso:**
```bash
# Reiniciar o Nginx e verificar se ele está rodando corretamente
sudo systemctl restart nginx
sudo systemctl status nginx
```

---

### 📦 Gerenciamento de Pacotes
Instale, atualize e remova softwares. Os comandos variam conforme a distribuição.

#### Debian / Ubuntu (apt)
```bash
# Atualiza a lista de pacotes disponíveis
sudo apt update

# Instala as atualizações dos pacotes
sudo apt upgrade

# Instala um novo pacote
sudo apt install curl

# Remove um pacote
sudo apt remove curl
```

#### CentOS / Fedora / RHEL (dnf ou yum)
```bash
# Atualiza todos os pacotes
sudo dnf upgrade

# Instala um novo pacote
sudo dnf install curl

# Remove um pacote
sudo dnf remove curl
```

---

### 🔐 Segurança e Acesso Remoto (SSH)
Conecte-se a servidores remotos de forma segura.

| Comando | O que faz? |
| :--- | :--- |
| **`ssh-keygen`** | **Criar um par de chaves SSH:** Gera uma chave privada (que fica com você) e uma pública (que você coloca no servidor) para login sem senha. |
| **`ssh-copy-id`**| **Copiar a chave pública:** A forma mais fácil de instalar sua chave pública em um servidor remoto. |
| **`ssh`** | **Conectar a um servidor:** Inicia uma conexão segura com um host remoto. |
| **`chmod`** | **Alterar permissões:** Modifica as permissões de leitura (r), escrita (w) e execução (x) de um arquivo ou diretório. |

**Exemplo de fluxo de trabalho para login sem senha:**
```bash
# 1. Crie suas chaves (só precisa fazer uma vez)
ssh-keygen -t rsa -b 4096 -C "seu_email@example.com"

# 2. Copie a chave pública para o servidor
ssh-copy-id usuario@ip_do_servidor

# 3. Conecte-se sem precisar de senha!
ssh usuario@ip_do_servidor

# Exemplo de permissão: torna um script executável
chmod +x meu_script.sh
```