FROM node:14 AS builder

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build-ts

FROM node:14-alpine AS server

WORKDIR /usr/src/app
RUN chown -R node:node /usr/src/app

USER node
EXPOSE 5001

COPY package*.json ./
RUN npm install --production

COPY --from=0 /usr/src/app/dist dist

ENV NODE_ENV=production

CMD ["node", "dist/server.js"]
