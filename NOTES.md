https://hub.docker.com/r/camilamaia/node

## Introdução ao Docker

Nessa aula você:
* conheceu a ideia de virtualização,
* entendeu o conceito de containers,
* descobriu o que é o Docker e suas principais tecnologias,
* instalou o Docker no sistema operacional,
* e o testou através de uma imagem Hello, World, que foi baixada do Docker Hub

Segue também uma breve lista dos comandos utilizados:

```bash
docker version # exibe a versão do docker.
docker run NOME_DA_IMAGEM # cria um container com a respectiva imagem passada como parâmetro.
```

## Trabalhando com imagens

Aprendemos neste capítulo:
* Comandos básicos do Docker para podermos baixar imagens e interagir com o container.
* Imagens do Docker possuem um sistema de arquivos em camadas (Layered File System) e os benefícios dessa abordagem principalmente para o download de novas imagens.
* Imagens são Read-Only sempre (apenas para leitura)
* Containers representam uma instância de uma imagem
* Como imagens são Read-Only os containers criam nova camada (layer) para guardar as alterações
* O comando Docker run e as possibilidades de execução de um container

Segue também uma breve lista dos comandos utilizados:

```bash
docker ps # exibe todos os containers em execução no momento.
docker ps -a # exibe todos os containers, independentemente de estarem em execução ou não.
docker run -it NOME_DA_IMAGEM # conecta o terminal que estamos utilizando com o do container.
docker start ID_CONTAINER # inicia o container com id em questão.
docker stop ID_CONTAINER # interrompe o container com id em questão.
docker start -a -i ID_CONTAINER # inicia o container com id em questão e integra os terminais, além de permitir interação entre ambos.
docker rm ID_CONTAINER # remove o container com id em questão.
docker container prune # remove todos os containers que estão parados.
docker rmi NOME_DA_IMAGEM # remove a imagem passada como parâmetro.
docker run -d -P --name NOME dockersamples/static-site # ao executar, dá um nome ao container.
docker run -d -p 12345:80 dockersamples/static-site # define uma porta específica para ser atribuída à porta 80 do container, neste caso 12345.
docker run -d -e AUTHOR="Fulano" dockersamples/static-site # define uma variável de ambiente AUTHOR com o valor Fulano no container criado.
```

## Trabalhando dados com volumes

Nessas aulas avançamos bastante e aprendemos:
* Que Container são voláteis, isso é, ao remover um, removemos os dados juntos
* Para deixar os dados persistente devemos usar Volumes
* Que volumes salvos não ficam no container e sim no Docker Host
* Como criar um ambiente de execução node.js

Segue também uma breve lista dos comandos utilizados:

```bash
docker run -v "CAMINHO_VOLUME" NOME_DA_IMAGEM # cria um volume no respectivo caminho do container.
docker inspect ID_CONTAINER # retorna diversas informações sobre o container.
```

## Construindo nossas próprias Imagens

Aprendemos neste capítulo:

* A entender o papel do arquivo DockerFile para criar imagens.
    * O Dockerfile define os comandos para executar instalações complexas e com características específicas.
* Vimos os principais comandos como `FROM`, `MAINTAINER`, `COPY`, `WORKDIR`, `RUN`, `EXPOSE` e `ENTRYPOINT`
* A subir uma imagem criada através de um Dockerfile para o Docker Hub e disponibilizar para os desenvolvedores

Lembrando também:

* as imagens são read-only sempre
* um container é uma instância de uma imagem
* para guardar as alterações a docker engine cria uma nova layer em cima da última layer da imagem

Segue também uma breve lista dos comandos utilizados:


```bash
docker build -f Dockerfile # Cria uma imagem a partir de um Dockerfile.
docker build -f CAMINHO_DOCKERFILE/Dockerfile -t NOME_USUARIO/NOME_IMAGEM
# constrói e nomeia uma imagem não-oficial informando o caminho para o Dockerfile.
docker login # inicia o processo de login no Docker Hub.
docker push NOME_USUARIO/NOME_IMAGEM # envia a imagem criada para o Docker Hub.
docker pull NOME_USUARIO/NOME_IMAGEM # baixa a imagem desejada do Docker Hub.
```

##  Comunicação entre containers

Neste capítulo aprendemos:
* Que imagens criadas pelo Docker acessam a mesma rede, porém apenas através de IP.
* Ao criar uma rede é possível realizar a comunicação entre os containers através do seu nome.
* Que durante a criação de uma rede precisamos indicar qual driver utilizaremos, geralmente, o driver bridge.

Segue também uma breve lista dos comandos utilizados:

```bash
hostname -i # mostra o ip atribuído ao container pelo docker (funciona apenas dentro do container).
docker network create --driver bridge NOME_DA_REDE # cria uma rede especificando o driver desejado.
docker run -it --name NOME_CONTAINER --network NOME_DA_REDE NOME_IMAGEM # cria um container especificando seu nome e qual rede deverá ser usada.
```


## Trabalhando com o Docker Compose

Nessa aula aprendemos:
    * A necessidade de usar o Docker Compose
    * Configurar o build de vários containers através do docker-compose.yml
    * Subir e parar os containers de maneira coordenada com Docker Compose

Segue também uma breve lista dos novos comandos utilizados:

```bash
docker-compose up # sobe os serviços criados
docker-compose down # para os serviços criados.
docker-compose ps # lista os serviços que estão rodando.
docker exec -it alura-books-1 ping node2 # executa o comando ping node2 dentro do container alura-books-1
```
