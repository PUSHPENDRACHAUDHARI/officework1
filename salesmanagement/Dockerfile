# ---------- Build Stage ----------
FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# ---------- Runtime Stage ----------
FROM nginx:alpine

# REMOVE default nginx files
RUN rm -rf /usr/share/nginx/html/*

# COPY correct Angular build output
COPY --from=build /app/dist/salesmanagement /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

