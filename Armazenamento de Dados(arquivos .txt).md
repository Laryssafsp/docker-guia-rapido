# Arquivos: 
## Exemplo - Apache Container
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

# Arquivos: 
## Exemplo - Tipos de mount, na prática
```
****bind mount *****

docker run -dti --mount type=bind,src=/opt/teste,dst=/teste debian

docker run -dti --mount type=bind,src=/opt/teste,dst=/teste,ro debian

***volumes****

docker volume create teste
docker volume ls

	/var/lib/docker/volumes/teste/_data
	
docker run -dti --mount type=volume,src=teste,dst=teste debian

docker volume rm teste
```

# Arquivos: 
## Exemplo - Montando (mount) um local de armazenamento
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
```
docker run -e MYSQL_ROOT_PASSWORD=Senha123 --name mysql-A -d -p 3306:3306 --volume=/data:/var/lib/mysql mysql
```
#### conexão com local
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
 --volume=/data:/var/lib/mysql mysql = host:container
