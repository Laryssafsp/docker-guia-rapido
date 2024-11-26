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

```docker stop [name]``` --> parar o container

```docker run``` 

```docker run -it ubuntu``` --> dentro do container (S.O) -  executar um conteiner com a imagem do ubuntu

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

```docker rm [name]```

--> o mesmo com as imagen
```docker images``` --> visualizar

```docker rmi [imagem]```

#### Chamar imagem
```docker tun -dti [imagem]```
Obs.: se voce pedir uma imagem que não encontra na máquina, então ele procura nos repositórios e realiza o download download

```docker run -dti --name Ubuntu-A ubuntu``` --> docker run -dti --name [container]-A [imagem]

```docker run -d```
Obs.: se sair do container, ele permanece a execução em background;
 
### Copiando arquivos para o contêiner
```docker exec -ti Ubuntu-A /bin/bash```

```docker exec Ubuntu-A mkdir /destino/``` --> criar diretorio dentro do container - não precisa estar dentro do bash
```docker exec Ubuntu-A mkdir ls -l /```

```nano Arquivo.txt --> entrar no namo e realizar applicaçoes dentro do container```

```ctrl x``` --> sair do nano

```docker cp arquivo.txt Ubuntu-A:/aula/``` ->> copiar arquivos e pastas entre container entre local e container:/diretorio

```docker exec Ubuntu-A mkdir ls /desino -l ``` ->> verifica se o arquivo esta no diretorio (cópia)

```exit```  --> sair do container (mas continua executando)
 
-- instalar
```apt -y install namo```

-- atualizar repositórios antes de instalar
```apt update```

```apt update -y```

#### Instalando o ZIP no container
```apt install -y zip  ```

```apt -y install zip  ```

#### para ZIPAR arquivos:
```zip NOME_COPILADO.zip *.txt``` ->> tudo que for .txt  NOME_COPILADO == Meuzip

```ls -l``` ->> listar arquivos da pasta

#### enviando para outro local
```docker cp NOME_COPILADO.zip Ubunto-A:/destino``` NOME_COPILADO == Meuzip

#### abrir a pasta para verificação
```docker exec -it Ubunto-A /bin/bash```

```cd /destino/```

```ls```
-->> para descompactar, será necessário instalar o ZIP na pasta
```unzip NOME_COPILADO.zip```

### Copiando arquivos do container para máquina local

```docker cp Ubuntu-A:/destino/Meuzip.zip  Zipcopia.zip``` -->> para o destino Zipcopia.zip

### TAGs
```docker pull debian:9``` ->> tag:versão

```docker run -dti debian:9``` ->> executar e gera um nome aleatório para o container

### Criando um contêiner do MySQL
já existe um container do MySQL com versões específicas
-- necessário específicar variáveis de ambiente

```docker pull mysql``` ->> chamar a imagem do MySQL

--> qual o host e set de variáveis
```docker run -e MYSQL_ROOT_PASSWORKS=Senha123 --name mysql-A -d -p 3306:3306 mysql``` -->> criar um banco de dados
--> MYSQL_ROOT_PASSWORKS=Senha123 = escolher a senha
-->> nome do comntainer = mysql-A 
-->> -d = execução em background
-->> -p 3306:3306 = libração de porta (padrão do MySQL) porta:porta_padrao nome_imagem

```docker exec -it musql-A bash``` -->> bash para realizar as configurações necessárias

```mysql -u root -p --protocol=tcp``` -->> acesso ao banco


```docker inspect mysql-A``` -->> informações da MV

### Parando e reiniciando um container
```docker stop mysql-A``` -->> parar de executar o container, porém ele ainda existe

```docker start mysql-A``` -->> reiniciar o container

```docker ps``` -->> verifica quem esta em execução

```docker rm mysql-A``` -->> excluir o container e perde os dados

-- se quer manter os dados, pode mapear o local de armazenamento dos dados

### Acessando um container externamente
```docker pull mysql```

```docker run -e MYSQL_ROOT_PASSWORD=Senha123 --name mysql-A -d -p 3306:3306 mysql``` 

```docker exec -it mysql-A bash```

```mysql -u root -p --protocol=tcp``` -->> acesso ao banco


```CREATE DATABASE aula;```

```show databases;```

```docker inspect mysql-A```

```mysql -u root -p --protocol=tcp```



