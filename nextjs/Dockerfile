FROM node:18

WORKDIR /app

COPY frontend/package.json frontend/package-lock.json ./

RUN npm install

RUN npm install -g nodemon

COPY frontend .

EXPOSE 3000

CMD ["nodemon", "-L", "--watch", ".", "--exec", "npm", "run", "dev"]