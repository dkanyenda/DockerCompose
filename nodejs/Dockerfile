
FROM ubuntu
WORKDIR /usr/app/src/app
COPY package*.json ./
RUN apt-get update && apt-get install -y curl
RUN apt install -y \
  curl
RUN apt install -y \
  nodejs
RUN apt-get install -y \
  npm
RUN echo "Node: " && node -v
RUN echo "NPM: " && npm -v
RUN npm install
COPY . .
EXPOSE 8080
CMD [ "node", "server.js" ]
