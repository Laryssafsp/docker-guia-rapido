# Arquivo Limitando Memória e CPU:

Visualizar container em andamento: ```docker ps```
Container name: php-A
status: ```docker stats php-A ``` ou ```stats php-A ```

Exemplo do status:
# Container Information

| **CONTAINER ID** | **NAME** | **CPU %** | **MEM USAGE / LIMIT** | **MEM %** | **NET I/O**     | **BLOCK I/O**    | **PIDS** |
|------------------|----------|-----------|-----------------------|-----------|-----------------|------------------|----------|
| d8949aee8f1f     | php-A    | 0.00%     | 9.602 MiB / 3.75 GiB  | 0.25%     | 3.71 kB / 24.4 kB | 1.27 MB / OB     | 7        |
| id do container   | nome   | requisições/uso     | memoria utilizada / limite de execução do container  | % memoria    |output da rede | qtd. inf. salva em disco     | qtd. processos        |

update no na memódia: ```docker update php-A -m 128M --cpus 0.2```
memória de: 128M
limite de processamento 20%

| **CONTAINER ID** | **NAME** | **CPU %** | **MEM USAGE / LIMIT** | **MEM %** | **NET I/O**     | **BLOCK I/O**    | **PIDS** |
|------------------|----------|-----------|-----------------------|-----------|-----------------|------------------|----------|
| d8949aee8f1f     | php-A    | 0.00%     | 9.602 MiB / 128Mib  | 7.5%     | 3.71 kB / 24.4 kB | 1.27 MB / OB     | 7        |

- específicando os dados na criação do container: ```docker run --name ubuntu-C -dti -m 128M --cpus 0.2 ubuntu ```

---

**O que o comando faz:**
O comando abre um terminal interativo (bash) dentro do container ubunto-C, permitindo que você execute comandos dentro do container, como se estivesse em uma máquina virtual ou servidor.
Se o nome do container for ubuntu-C, o comando correto seria:

``docker exec -ti ubuntu-C bash``

#### Explicação dos parâmetros:

`docker exec`: Este comando é utilizado para executar um comando dentro de um container em execução.

`-t`: Aloca um terminal TTY (teletipo). Isso cria uma interface interativa no terminal, permitindo que você interaja com o container como se estivesse em um terminal físico.

`-i`: Mantém a entrada interativa aberta. Isso permite que você interaja com o processo dentro do container.

`ubunto-C`: Este é o nome ou ID do container onde o comando será executado. (Observe que parece haver um erro de digitação aqui; o correto seria ubuntu-C, caso esteja se referindo a um container baseado na imagem Ubuntu).

`bash`: Este é o comando a ser executado dentro do container. No caso, o comando inicia uma nova sessão de terminal usando o bash, que é um shell de comandos.

---

Agora o stress estará disponível dentro do seu container para ser utilizado, permitindo que você gere carga no sistema para testes de desempenho ou outros fins.
```apt update && apt install stress```

#### Stress
Resumo do que o comando faz: 
```stress --cpu 1 --vm-bytes 50m --vm 1 --vm-bytes 50m```

Geração de carga na CPU: O stress usará 1 núcleo de CPU realizando cálculos intensivos.
Geração de carga na memória: O stress aloca 50 MB de memória RAM (usando o parâmetro --vm-bytes 50m) e cria 1 processo para consumir essa memória (usando o parâmetro --vm 1).

**O que isso pode causar?**
Este comando simula uma carga leve na CPU (por usar apenas 1 núcleo) e na memória (alocando 50 MB), útil para testar o comportamento do sistema sob estresse moderado.

Caso você queira aumentar a carga, pode aumentar os valores desses parâmetros, como por exemplo:

Aumentar o número de CPUs com --cpu 2 ou mais.
Aumentar o número de processos de memória com --vm 2 ou mais.
Aumentar a quantidade de memória com --vm-bytes 100m ou mais.
Este comando é útil em testes de desempenho ou stress para verificar como o sistema lida com carga de CPU e memória.

  
---
# Informações, logs e processos

```docker info```: informações sobre o servidor <br>
```docker ps``` : lista os existentem <br>
```docker container logs [nome]```: log de execuçaõ do [nome] <br>
```docker container top [nome container]```: processos em execução no container <br>

---

# Redes:

```docker network ls```: redes disponíveis <br>
```docker network inspect bridge```: containers disponíveis na rede <br>
```docker network inspect [rede]```: containers especificos disponíveis na rede <br>
```apt-get install iputils-ping``` : O comando apt-get install iputils-ping instala o utilitário ping no seu sistema, permitindo que você possa usar o ping para testar a conectividade de rede com outros dispositivos e hosts.<br>
```docker network create minha-rede```: Cria uma rede e especifica uma subrede para essa rede criada <br>
```docker run -dit --name Ubuntu-B --network minha-rede  ubuntu ```: criando container específicando a rede.

* Consegue comunicação com container se estiverem no mesmo IP, isolando quando expecifica-se a rede

# Quesçoes:

- 1/4: Qual comando pode ser utilizado para listar todos os containers em execução? ``` docker container ls```

- 2/4: Qual comando pode ser utilizado para listar todas as imagens disponíveis em um host? ```docker image ls```

- 3/4: Qual comando é utilzado para atualizar a quantidade de memória em 128 megabytes em um container com o nome de php-A? ```docker update php-A -m 128M```

- 4/4: Qual aplicação podemos utilizar para realizar um teste de stress no container? ```stress```
