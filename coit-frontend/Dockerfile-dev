FROM node:16.13.1 AS build
WORKDIR /usr/app
COPY . /usr/app
RUN npm install
RUN npm run build


FROM nginx
COPY --from=build /usr/app/build /usr/share/nginx/html
