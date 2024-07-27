# Fase de construção
FROM maven:3.8.6-openjdk-18 AS builder

# Diretório de trabalho dentro do container
WORKDIR /app

# Clonar o repositório Git público
RUN git clone https://github.com/nintendowiiu2712/rafael

# Mudar para o diretório do repositório clonado
WORKDIR /app/rafael/DockerRafael

# Verificar se o POM está no diretório correto
RUN ls -la

# Compilar o projeto e instalar as dependências
RUN mvn clean install

# Fase de execução
FROM openjdk:18-jdk-slim

# Diretório de trabalho dentro do container
WORKDIR /app

# Copiar o artefato JAR do estágio de build para o estágio final
COPY --from=builder /app/rafael/DockerRafael/target/*.jar app.jar

# Expor a porta 8080
EXPOSE 8080

# Comando para iniciar a aplicação
ENTRYPOINT ["java", "-jar", "app.jar"]
