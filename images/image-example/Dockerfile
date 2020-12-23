FROM node:12-alpine

WORKDIR /usr/src/app

ARG package=package*.json
COPY $package ./

ARG yarnlock=yarn.lock
COPY $yarnlock ./

ARG tsconfig
COPY --chown=node:node $tsconfig ./

ARG src=.
ADD --chown=node:node $src .

RUN yarn

ARG tsconfig=tsconfig.json
ENV TSCONFIG=$tsconfig

RUN yarn build

CMD ["yarn", "start"]
