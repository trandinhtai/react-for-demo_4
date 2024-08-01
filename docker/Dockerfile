# build stage 
FROM node:8.9.4-alpine as build-stage

RUN mkdir /app
WORKDIR /app

COPY package.json /app

RUN npm install 

COPY . /app

# RUN npm run test

RUN npm run build 
RUN ls -alh

# production stage
FROM nginx:1.17-alpine as production-stage
COPY --from=build-stage /app/build /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]
