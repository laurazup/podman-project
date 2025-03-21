# Podman Project - Web Server and Database Setup

Este projeto demonstra como configurar um servidor web simples usando Nginx e um banco de dados PostgreSQL com Podman e Podman Compose.

## Estrutura do Projeto
```
.
├── podman-compose.yaml
├── Podfile
├── html
│ └── index.html
└── data
```

### Descrição dos Arquivos 
1. **podman-compose.yaml**: Define os serviços do projeto (servidor web e banco de dados). 
2. **Podfile**: Especifica a configuração para o container Nginx. 
3. **html/index.html**: Um arquivo HTML simples que será servido pelo servidor Nginx. 
4. **data/**: Diretório para persistir os dados do banco de dados PostgreSQL. 

--- 

## Pré-requisitos 
1. **Podman** e **Podman Compose** instalados no sistema. 
2. Conhecimento básico sobre aplicações containerizadas. 

---

## Executando a Aplicação

### 1. Construir e Iniciar os Containers

Execute o seguinte comando para construir e iniciar os containers:
```
podman-compose up
```

### 2. Verificar os Containers em Execução

Use o comando abaixo para verificar se os containers estão em execução:
```
podman ps
```

Exemplo de saída:

```
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES 
b179606d3d6a localhost/podman-project_web:latest nginx -g daemon o... 5 minutes ago Up 27 seconds 0.0.0.0:8080->80/tcp podman-project_web_1 
0ac6b56b7aa9 docker.io/library/postgres:latest postgres 5 minutes ago Up 23 seconds podman-project_db_1
```

### 3. Acessar o Servidor Web
Abra o navegador e acesse:

http://localhost:8080

Você verá a mensagem: "Olá, Mundo!"

## Interagindo com o Banco de Dados

### 1. Acessar o Container Web
Entre no container do serviço web:
```
podman exec -it podman-project_web_1 sh
```

### 2. Instalar o Cliente PostgreSQL
Instale o cliente PostgreSQL dentro do container:
```
apk add --no-cache postgresql-client
```

Exemplo de saída:

```
fetch https://dl-cdn.alpinelinux.org/alpine/v3.21/main/x86_64/APKINDEX.tar.gz 
fetch https://dl-cdn.alpinelinux.org/alpine/v3.21/community/x86_64/APKINDEX.tar.gz 
(1/5) Installing postgresql-common (1.2-r1) ... OK: 48 MiB in 72 packages
```
3. Conectar ao Banco de Dados
Use o comando psql para conectar ao banco de dados:
```
psql -h db -U postgres -d mydb
```

Quando solicitado, insira a senha: postgres.

Exemplo de saída:
```
psql (17.4) Type "help" for help. 
mydb=#
```

### 4. Explorar o Banco de Dados
Listar todos os bancos de dados:
```
\l
```

Listar todas as relações (tabelas, views, etc.):
```
\d
```

Sair do shell do banco de dados:
```
exit
```
Sair do shell do container:
```
exit
```

## Resumo

Este projeto demonstra como:

- Configurar um servidor web usando Nginx.
- Configurar um banco de dados PostgreSQL.
- Interagir com o banco de dados a partir do container web.