## GIT

- Criar repositório 

```
$ git init
```

- Configurar repositório local (projeto)

```
$ git config --local user.name "Seu nome aqui"
$ git config --local user.email "seu@email.aqui"
```

- Visualizar  Usuário Configurado 

```
$ git config -l
```

- Enviar Arquivos

```
$ git commit -m “<COMENTARIO>”
$ git push origin master
```

- Receber Arquivos

```
$ git pull origin master
```

- Aumentar Tamanho do Buffer de Envio

```
git config http.postBuffer 524288000
```

- Verificar situação dos arquivos

```
$ git status
```

- Criar Branch

```
$ git branch <NOME_DA_BRANCH>
```

- Criar Branch e mudar para branch criada

```
$ git checkout -b <NOME_DA_BRANCH>
```

- Mudar de Branch

```
$ git checkout <NOME_DA_BRANCH>
```

- Listar Branches remotas do repositório 

```
$ git branch -r
```

- Listar Branches remotas e local do repositório 

```
$ git branch -a
```

- Criar Branch remota 

```
$ git push -u origin <NOME_DA_BRANCH>
```

- Apagar uma Branche remota 

```
$ git push -d origin <NOME_DA_BRANCH>
```

- Verificar a atualizações realizadas no repositório

```
$ git fetch origin 
$ git fetch <NOME_DO_REPOSITORIO>
```

- Descartar alterações em um arquivo

```
$ git checkout <NOME_DO_ARQUIVO>
```

- Descartar alterações do arquivo no INDEX

```
$ git reset HEAD <NOME_DO_ARQUIVO>
```

- Descartar alterações definitiva do último COMMIT

```
$ git reset --hard HEAD~1
```

- Salvar as alterações do Working Directoy e INDEX

```
$ git stash
```

- Visualizar alterações na STASH 

```
$ git stash list
```

- Remover última alteração na STASH 

```
$ git stash pop
```

- Remover determinado item na STASH

```
$ git stash drop <NUMERO>
```

- Listar ferramentas de Merge

```
$ git mergetool --tool-help
```

- Reiniciar credenciais do windows

```
$ git config --global credential.helper wincred
```

- Copiar COMMIT e adicionar a INDEX

```
$ git cherry-pick -n <NUMERO_DO_COMMIT>
```

- Atualizar git no Windows

```
$ git update-git-for-windows
```

- Criar TAG (Release)

```
$ git tag -a <NOME_DA_VERSAO> -m <MENSAGEM>
$ git push origin <NOME_DA_VERSAO>
```

- Apagar TAG (Release)

```
$ git tag -d <NOME_DA_VERSAO>
```

- Trocar URL do repositório

```
$ git remote -v
$ git remote set-url origin git@hostname:USERNAME/REPOSITORY.git
$ git remote set-url origin https://hostname/USERNAME/REPOSITORY.git
```

- Formatar mensagens do histórico (http://devhints.io/git-log)

```
$ git log --pretty="format:%h %s"
```

- Configuração de Push Notification (Arquivo $GIT_DIR/hooks/post-receive)

```
curl http://endereco.do.jenkins/git/notifyCommit?url="https://github.com/fsaires/<NOME_DO_REPOSITORIO>.git"
```

- Apagar a pasta do git em todo diretório

```
$ rm -r pt-br/.git/
```

```
$ git credential reject protocol=https host=github.com
```
