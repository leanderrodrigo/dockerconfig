# Como instalar o Docker para windows 10

<p>
<br/>

<br/>

### Primeiramente clique na imagem abaixo:

[![Docker](https://pplware.sapo.pt/wp-content/uploads/2019/03/docker_01-1-720x332.jpg)](https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe) <br/>Docker version 19.03.5, build 633a0ea 

<br/>

### Após a instalação do Docker, utilizando o Powershell ou cmd, digite os seguintes comandos abaixo:
### Caso tenha pressa, baixar os bats no link ao lado: [[Bats]](https://github.com/Guinocencio/ConfDocker/blob/master/Bats/Bats.rar?raw=truee)

<br/>

<br/>

**1. docker network create elknetwork**

<br/>

**2. docker run -d --name elasticsearch7 --net elknetwork -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.4.2**

<br/>

**3. docker run -d --name kibana --net elknetwork --link elasticsearch7:elasticsearch -p 5601:5601 kibana:7.4.2**

<br/>

##### Para instalar o modulo de logs
**docker run -d --name logstash7 --restart=always --net elknetwork --link elasticsearch7:elasticsearch -p 5000:5000 logstash:7.4.2 --path.settings= -e 'input { tcp { port => 5000 codec => "json" } } output { elasticsearch { hosts => ["elasticsearch"] index => "micro-%{serviceName}"} }'**
<br/>

##### Na pasta environment tem a imagem do REDIS (nosso cache provider) na pasta raiz do projeto(C:\Users\user-name\Documents\project-cida-services) executem:
**docker-compose -f environment/redis.yaml up -d**
<br/>

#### Caso aparecer este erro ("Error response from daemon: could not find plugin bridge in v1 plugin registry: plugin not found") rodar o comando ao lado: **"docker network create -d bridge elknetwork"** 
<br/>

![1](https://github.com/Guinocencio/ConfDocker/blob/master/img/1.png) 

<br/>

**Imagem 1:** mostra a utilização do comando 1 após utilizar **"docker network create -d bridge elknetwork"**.

![2](https://github.com/Guinocencio/ConfDocker/blob/master/img/2.png) 

<br/> 

**Imagem 2:** mostra a instalação dos comandos 2 e 3.

![](https://github.com/Guinocencio/ConfDocker/blob/master/img/3.png) 

<br/>
<br/>

Após rodar o comando **"docker ps"** aparecerá uma lista.
Caso os containers tenham sido instalado com sucesso aparecerá uma lista como esta acima.


<p/>
