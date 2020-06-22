## POSTGRES

- START:

```
$ pg_ctl -D "C:\Program Files\PostgreSQL\9.6\data" start
```

- STOP:

```
$ pg_ctl -D "C:\Program Files\PostgreSQL\9.6\data" stop -s
```

- RESTART:

```
$ pg_ctl -D "c:/Program Files/PostgreSQL/9.2/data" restart
```

- Logar

```
$ su - postgres
```

 - Prompt

```
psql
```

- Listar Databases

```
\l
```

- Sair

```
\q
```

- Conectar no Banco

```
\c nomebanco
```

- Listar Tabelas

```
\dt
```

- Reiniciar Sequence Tabelas

```
ALTER SEQUENCE nome_sequence RESTART WITH 1;
```

- Exibir enconding

```
SHOW SERVER_ENCODING;
```

```
SHOW SERVER_ENCODING;
```