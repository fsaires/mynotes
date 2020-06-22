## DOCKER

- Exibir todos os containers, independentemente de estarem em execução ou não: 

```
$ docker ps -a
```

- Download de uma imagem: 

```
$ docker pull <NOME_DA_IMAGEM>
```

- Informações container: 

```
$ docker inspect <ID_CONTAINER>
```

- Subir um container: 

```
$ docker start <ID_CONTAINER>
```

- Parar um container: 

```
$ docker stop <ID_CONTAINER>
```

- Parar todos containers ativos: 

```
$ docker stop $(docker ps -q)
```

- Entrar no Container: 

```
$ docker attach <ID_CONTAINER>
```

- Remover container:  

```
$ docker rm <ID_CONTAINER>
```

- Remover imagem: 

```
$ docker rmi <ID_DA_IMAGEM> <NOME_DA_IMAGEM>
```

- Commit imagem

```
$ docker commit <NOME_DO_CONTAINER> <NOME_DA_IMAGEM>
```

- Gerar uma nova imagem 

```
docker build -t <NOME_DA_IMAGEM> .
```

- Enviar imagem Docker Hub

```
$ docker push <NOME_DA_IMAGEM>
```

- Exportar uma imagem para TAR

```
$ docker save fsaires/myserverphp7.1 > e:\myserverphp7.1.tar
```

- Importar imagem em arquivo TAR

```
$ docker load < e:\myserverphp7.1.tar
```

- Versionamento Imagem (TAG)

```
$ docker tag 18d86a2f57ba fsaires/myserverphp7.1:1.0
```

- Remover imagens, container e cache

```
$ docker system prune -a
```

- Remover todos os comandos inativos

```
$ docker container prune
```

- Verificar as portas do Container

```
$ docker port <ID_CONTAINER>
```

- Retornar o ID dos Containers ativos

```
$ docker ps -q
```

- Criando uma rede 

```
$ docker network create --driver bridge <NOME_DA_REDE>
```

- Listar redes 

```
$ docker network ls
```

- Verificar o IP do Container (Dentro do Container):

```
$ hostname -i
```

- Iniciar serviços criados

```
$ docker-compose up
$ docker-compose up -d
```

- Parar serviços criados

```
$ docker-compose down
```

- Reiniciar serviços criados

```
$ docker-compose restart
```

- Listar serviços em execução

```
$ docker-compose ps
```
