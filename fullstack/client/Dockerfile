FROM node:22

ENV NODE_OPTIONS="--openssl-legacy-provider"

WORKDIR /client

COPY package*.json /client/

RUN npm install

COPY . /client/

EXPOSE 3000

CMD [ "npm", "start"]