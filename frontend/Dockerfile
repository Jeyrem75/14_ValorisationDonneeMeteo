FROM bellsoft/hardened-nodejs:24-musl AS build

WORKDIR /app
RUN chown node:node /app
USER node

COPY --chown=node:node package*.json .

RUN npm install

COPY --chown=node:node . .

RUN npm run build

FROM bellsoft/hardened-nodejs:24-musl AS prod

WORKDIR /app
RUN chown node:node /app
USER node

COPY --from=build --chown=node:node /app/.output /app/.output

ENV NODE_ENV=production

EXPOSE 3000

CMD [ "node", ".output/server/index.mjs" ]
