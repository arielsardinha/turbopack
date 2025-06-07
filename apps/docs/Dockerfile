FROM node:22.15.0

WORKDIR /usr/src/app

COPY . .
RUN npm i
RUN npm run build --prefix ./apps/docs

EXPOSE 3000

CMD [ "npm", "run", "start", "--prefix", "./apps/docs"]