FROM node:20-alpine

WORKDIR /app

COPY backend/package*.json ./

RUN npm install

copy backend .

EXPOSE 5000

CMD ["npm","start"]
