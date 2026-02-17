FROM node:23-alpine3.19 as build
WORKDIR /nsse-frontend 
COPY package*.json .
RUN npm ci --silent --only=production
COPY . .
RUN npm run build

FROM nginx:1.29.5-alpine
COPY --from=build /nsse-frontend/dist /usr/share/nginx/html
# Removing default URI paths in nginx
RUN rm /etc/nginx/conf.d/*
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]


