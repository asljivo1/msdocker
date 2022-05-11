FROM ubuntu:18.04 as clone 

RUN apt-get -y update && \
    apt-get -y install git && \
    git clone https://github.com/kkenan/basic-microservices.git

FROM node:9-alpine

ENV APPDIR /app

WORKDIR ${APPDIR}

COPY --from=clone /basic-microservices/node-app/index.js ${APPDIR}/
COPY --from=clone /basic-microservices/node-app/package*.json ${APPDIR}/

RUN npm install

EXPOSE 8081
CMD [ "node", "index.js" ]

