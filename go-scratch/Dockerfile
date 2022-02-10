
## Uma vez que Go é uma linguagem compilavel, eu posso simplesmente
## usar uma imagem do Go para compilar a aplicacao e pegar
## a aplicacao compilada e jogar em uma imagem nova sem nada!
FROM golang:1.17.6-alpine3.14 as base

WORKDIR /usr/src


## Copiar todo conteudo da pasta para a imagem
COPY . .

### CGO desabilitar cross platform
ENV CGO_ENABLED=0

## setar que a aplicacao será rodada em linux
RUN GOOS=linux go build ./main.go

## jogar a aplicacao compilada em go para um imagem scratch de docker
FROM scratch

## tentei usar versoes do alpine porém ficou com algo próximo de 7MB

### Set working directory
WORKDIR /usr/src

### Copy built binary application from 'builder' image
COPY --from=base /usr/src/main .

### Run the binary application
CMD ["/usr/src/main"]