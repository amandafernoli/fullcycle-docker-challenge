# -- build stage --
FROM golang:1.7.3 AS builder

WORKDIR /var/app/

# Copia o código fonte do diretório atual para o diretório /app no contêiner
COPY ./src /var/app/

# Compila o aplicativo Go
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o go-app .


# -- final stage --
# imagem base mais leve
FROM scratch

# Define a variável de ambiente GO111MODULE para 'off'
ENV GO111MODULE=off

# Adiciona certificados CA
# RUN apk --no-cache add ca-certificates

# Copia o binário compilado do estágio de compilação para o estágio final
COPY --from=builder /var/app/go-app /var/app/go-app

WORKDIR /var/app/

# Executa o binário go-app
CMD ["./go-app"]