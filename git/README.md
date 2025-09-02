# 🐙 Guia de Comandos Git: O Essencial para seu Controle de Versão

Git é a ferramenta mais poderosa para controle de versão, permitindo que você e sua equipe trabalhem em projetos de forma organizada, segura e eficiente.

Este guia agrupa os comandos mais úteis por categoria, do básico ao avançado, para você ter sempre à mão.

---

### 🚀 Configuração Inicial e Repositórios
Primeiros passos para configurar seu ambiente e iniciar um repositório.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git init`** | **Criar um repositório:** Inicia um novo repositório Git no diretório atual. | `git init` |
| **`git config --global`** | **Configurar usuário (Global):** Define suas informações de autor para **todos** os repositórios na sua máquina. Faça isso uma vez! | `git config --global user.name "Seu Nome"` |
| **`git config --local`** | **Configurar usuário (Local):** Define suas informações para o repositório atual. Sobrescreve a configuração global. | `git config --local user.email "seu@email.aqui"` |
| **`git config -l`** | **Visualizar configurações:** Lista todas as configurações do Git (locais e globais) que estão aplicadas. | `git config -l` |
| **`git remote set-url`**| **Trocar URL remota:** Altera o endereço do repositório remoto (ex: ao migrar do HTTPS para SSH). | `git remote set-url origin git@github.com:user/repo.git` |

---

### 🔄 O Ciclo Básico do Dia a Dia
Os comandos que você usará 90% do tempo.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git status`** | **Verificar status:** Mostra o estado dos seus arquivos: quais foram modificados, quais estão no *stage* e quais não estão sendo rastreados. | `git status` |
| **`git add`** | **Adicionar ao Stage:** Prepara os arquivos modificados para serem incluídos no próximo commit. O *stage* (ou índice) é uma área de preparação. | `git add .` (adiciona tudo) ou `git add nome_do_arquivo.txt` |
| **`git commit`** | **Salvar alterações (Commit):** Grava permanentemente as alterações do *stage* no histórico do repositório com uma mensagem descritiva. | `git commit -m "Adiciona funcionalidade de login"` |
| **`git push`** | **Enviar para o remoto:** Envia seus commits locais para o repositório remoto (como GitHub ou GitLab). | `git push origin main` |
| **`git pull`** | **Receber do remoto:** Baixa as atualizações do repositório remoto e mescla (faz *merge*) com seu branch local. | `git pull origin main` |

---

### 🌿 Trabalhando com Branches
Organize seu trabalho em linhas de desenvolvimento paralelas.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git branch`** | **Listar branches locais:** Mostra todas as branches do seu repositório local e destaca a atual. | `git branch` |
| **`git branch <nome>`** | **Criar uma branch:** Cria uma nova branch a partir da sua posição atual. | `git branch nova-feature` |
| **`git checkout <nome>`** | **Mudar de branch:** Troca para a branch especificada. | `git checkout nova-feature` |
| **`git checkout -b <nome>`**| **Criar e mudar de branch:** Executa os dois comandos acima em um só passo. | `git checkout -b fix/bug-login` |
| **`git branch -a`** | **Listar todas as branches:** Mostra tanto as branches locais quanto as remotas. | `git branch -a` |
| **`git push -u origin <nome>`**| **Criar branch remota:** Envia sua nova branch local para o repositório remoto e estabelece um vínculo (`-u`). | `git push -u origin nova-feature` |
| **`git push -d origin <nome>`**| **Apagar uma branch remota:** Deleta a branch especificada no repositório remoto. | `git push -d origin feature-antiga` |

---

### ⏪ Desfazendo Alterações
Volte no tempo e corrija seus erros.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git checkout <arquivo>`** | **Descartar alterações locais:** Reverte um arquivo ao seu estado do último commit. **CUIDADO: as alterações são perdidas.** | `git checkout -- index.html` |
| **`git reset HEAD <arquivo>`** | **Tirar do Stage:** Remove um arquivo da área de *stage*, mas mantém as modificações no seu diretório de trabalho. | `git reset HEAD arquivo.js` |
| **`git reset --hard HEAD~1`** | **Desfazer o último commit:** **CUIDADO!** Apaga o último commit e **TODAS** as alterações associadas a ele de forma definitiva. | `git reset --hard HEAD~1` |
| **`git cherry-pick -n`** | **Copiar um commit:** Pega as alterações de um commit específico de outra branch e as aplica na sua branch atual, sem criar um novo commit (`-n`). | `git cherry-pick -n <HASH_DO_COMMIT>` |

---

### 📥 Stash: Guardando Alterações Temporariamente
Precisa mudar de branch, mas seu trabalho não está pronto para um commit? Use o `stash`!

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git stash`** | **Salvar alterações:** Guarda suas modificações locais (não commitadas) em uma "gaveta" temporária, limpando seu diretório de trabalho. | `git stash` |
| **`git stash list`** | **Visualizar o stash:** Mostra a lista de todas as alterações que você guardou. | `git stash list` |
| **`git stash pop`** | **Restaurar alterações:** Pega as últimas alterações guardadas no stash, as aplica de volta ao seu diretório e as remove da lista. | `git stash pop` |
| **`git stash drop`** | **Remover item do stash:** Descarta um conjunto de alterações guardado no stash. | `git stash drop stash@{1}` |

---

### 🔖 Tags e Releases (Versionamento)
Marque pontos importantes no histórico, como versões de lançamento.

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git tag -a`** | **Criar uma tag:** Cria uma tag anotada (`-a`) para marcar uma versão. | `git tag -a v1.0.0 -m "Lançamento da primeira versão"` |
| **`git push origin <tag>`**| **Enviar tag para o remoto:** Por padrão, tags não são enviadas. É preciso enviá-las explicitamente. | `git push origin v1.0.0` |
| **`git tag -d`** | **Apagar uma tag local:** Deleta uma tag da sua máquina. | `git tag -d v1.0.0` |

---

### 🛠️ Comandos Avançados e Utilitários

| Comando | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| **`git fetch`** | **Verificar atualizações:** Baixa as novidades do repositório remoto, mas **não** as mescla no seu branch local. Permite que você veja o que os outros fizeram antes de integrar. | `git fetch origin` |
| **`git log --pretty`** | **Formatar o histórico:** Exibe o histórico de commits de forma personalizada e mais legível. | `git log --pretty="format:%h %s" --graph` |
| **`git config http.postBuffer`**| **Aumentar buffer de envio:** Aumenta o limite de memória para operações de push, útil para repositórios muito grandes. | `git config --global http.postBuffer 524288000` |
| **`git config credential.helper`**| **Gerenciador de credenciais:** Configura um assistente para salvar suas credenciais (usuário/senha) e não precisar digitá-las toda vez. | `git config --global credential.helper wincred` (Windows) |