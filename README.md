# ![Docker](https://img.shields.io/badge/-docker-0D1117?style=for-the-badge&logo=docker&labelColor=0D1117)&nbsp; guia rapido!

### chamar/executar uma imagem docker:
```docker run image_name```

### imagens disponíveis
```docker images```
obs.: created é a data criada da imagem, nao no computador

### listar containers em execução
```docker ps```
ou
```docker container ls```

### listar container executado recentemente / estão ou não em executação.
```docker ps -a```
obs.: created: é a data criada da imagem na maquina

### Executando um contêiner
```docker pull ubuntu``` --> chamar imagem de um sistema operacional linux
```docker run ubuntu```
```docker run ubuntu sleep 10``` --> periodo parado
```docker run ubuntu sleep 1500``` --> periodo parado
```docker stop [id]``` --> parar o container
```docker run``` 
```docker run -it ubuntu``` --> dentro do container (S.O)

### Executando opções de ajuda
```docker --help ```
```docker container --help```

### Executando aplicações no contêiner
```docker run -dti  ubuntu [nome da imagem]```
```docker exec -it [id ou nome]  /bin/bash ```
obs.: entra no container, não precisa colocar o iD todo se o numero informado for único
```docker exec -it [id ou nome] cat /etc/\*reselase*```
obs.: entra no container, realiza o comando e fecha a execução
 
### Excluindo e nomeando contêineres
--> o contaniner pode nao esta em execução mas ocupa espaço/recursos 
```docker stop [id]```
```docker rm [id]```

--> o mesmo com as imagen
```docker images``` --> visualizar
```docker rmi [imagem]```

### Chamar imagem
```docker tun -dti [imagem]```
Obs.: se voce pedir uma imagem que não encontra na máquina, então ele procura nos repositórios e realiza o download download

```docker run -dti --name Ubuntu-A ubuntu```
```docker run -d```
Obs.: se sair do container, ele permanece a execução em background;
 
### Copiando arquivos para o contêiner
```docker exec -ti Ubuntu-A /bin/bash```
```docker exec Ubuntu-A mkdir /destino/```
```docker exec Ubuntu-A mkdir ls -l /```
```nano Arquivo.txt --> entrar no namo e realizar applicaçoes dentro do container```
```ctrl x``` --> sair do nano
```docker cp arquivo.txt Ubuntu-A:/aula/```
```exit```  --> sair do container (mas continua executando)
 
-- instalar
apt -y install namo

-- atualizar repositórios antes de instalar
apt update
apt update -y

### Copiando arquivos do container
```docker cp Ubuntu-A:/destino/Meuzip.zip  Zipcopia.zip```
 
### Criando um contêiner do MySQL
```docker cp Ubuntu-A:/destino/Meuzip.zip  Zipcopia.zip```
 
### Acessando um container externamente
```docker pull mysql```
```docker run -e MYSQL_ROOT_PASSWORD=Senha123 --name mysql-A -d -p 3306:3306 mysql```
```docker exec -it mysql-A bash```
```mysql -u root -p --protocol=tcp```


```CREATE DATABASE aula;```
```show databases;```

```docker inspect mysql-A```
```mysql -u root -p --protocol=tcp```
