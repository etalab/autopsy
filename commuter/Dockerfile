FROM node:10

WORKDIR /app

RUN git clone https://github.com/nteract/commuter

WORKDIR /app/commuter

RUN yarn

ENV COMMUTER_LOCAL_STORAGE_BASEDIRECTORY /notebooks 

EXPOSE 4000

CMD npm run start
