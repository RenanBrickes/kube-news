# Imagem base do container e tag de versão
FROM node:18.11.0
# Diretorio da aplicação
WORKDIR /app
# Copia do arquivo com todos pacote da aplicação
COPY package*json ./
# Comand de instalçao do pacote da aplicação
RUN npm install
# Copia do restante dos arquivos da aplicação
COPY . .
# Exposição da porta da aplicação
EXPOSE 8080
# Comando de execução da aplicação
CMD ["node", "server.js"]