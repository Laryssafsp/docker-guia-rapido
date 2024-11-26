# 1 - Exemplo - Montando (mount) um local de armazenamento
caso perca o container, pode recuperar os dados armazenados localmente
#### verificar dados
```docker inspect -A```
#### Diretório de onde o MYSQL esta dentro do container -->> 
```
Mounts [{...
  Type: volume
  Destination : diretório
...}]
```
#### criar pasta
```
mkdir /pasta
mkdir /pasta/mysql-A
```
#### salvar local
se perder o container, consegue recuperar os dados em outro container indicando este caminho

```
docker run -e MYSQL_ROOT_PASSWORD=Senha123 --name mysql-A -d -p 3306:3306 --volume=/data:/var/lib/mysql mysql
```
-->> volume=/data:/var/lib/mysql mysql = host:container

#### conexão com local

logar como root
```
mysql -u root -p --protocol=tcp --port=3306
```
```
CREATE TABLE alunos (
    AlunoID int,
    Nome varchar(50),
    Sobrenome varchar(50),
    Endereco varchar(150),
    Cidade varchar(50)
);

INSERT INTO alunos (AlunoID, Nome, Sobrenome, Endereco, Cidade) VALUES (1, 'Carlos Alberto', 'da Silva', 'Av. que sobe e desce que ninguém conhece', 'Manaus');
```


 ### recuperando dados local

``` docker ps ```--> listar containers

``` docker stop mysql ```--> parar container

``` docker rm mysql-A ```--> remover comtainer

```docker run -e MYSQL_ROOT_PASSWORD=Senha123 --name mysql-A -d -p 3306:3306 --volume=/data/mysqk-A:/var/lib/mysql mysql ``` --> mapeando a pasta locak


# 2 - Tipos de mount, na prática

**bind mount**

As montagens Bind sao basicamente apenas vincular um determinado
diretório ou arquivo do host dentro do contêiner (diretório específico): ``` docker run -v /hostdir:/containerdir mysql ```

**Volumes** nomeados são volumes que você cria manualmente com o
comando: ```docker volume create nome-do-volume```

Eles são criados em ```/var/lib/docker/``` volumes e podem ser referenciados
apenas por seu nome.
--> var = cria no dretório padrao do docker

Digamos que você crie um volume chamado "mysql_data", você pode apenas
referenciá-lo como o comando: ``` docker run -v mysql_data:/containerdir mysql```

**Dockerfile Volume**
Tipo de volume que são criados pela instrução VOLUME. Esses volumes
também são criados em ```/var/lib/docker/ volumes```, mas não têm um
determinado nome. 
O volume é criado ao executar o contêiner e são úteis
para salvar dados persistentes. O desenvolvedor pode dizer onde estão os
dados importantes e o que deve ser persistente.


**Qual devo utilizar?**
Depende de você. 
Se você quiser manter tudo na "área do docker" ```/var/lib/docker```, você pode usar volumes. 
Se você deseja manter sua própria estrutura de diretório, você pode usar binds.

- O Docker recomenda o uso de volumes em vez do uso de binds, pois os volumes são criados e gerenciados pelo docker.

---

Com o diretório específico:
```
docker run -dti --mount type=bind,src=/opt/teste,dst=/teste debian
```
com o diretório específico apenas para leitura dos arquivos [read only]
```
docker run -dti --mount type=bind,src=/opt/teste,dst=/teste,ro debian
```
***volumes***
```
docker volume create teste
docker volume ls
/var/lib/docker/volumes/teste/_data
	
docker run -dti --mount type=volume,src=teste,dst=teste debian

docker volume rm teste
```

# Apache Container
```
docker run  --name apache-A -d -p 80:80 --volume=/data/apache-A:/usr/local/apache2/htdocs/ httpd
docker run  --name php-A -d -p 8080:80 --volume=/data/php-A:/var/www/html php:7.4-apache

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8"/>
<title>Exemplo Apache</title>
</head>
<body>
<h1> OK !! Apache funcionando!!!!! </h1>
</body>
</html>

<?php
phpinfo();
?>
```

