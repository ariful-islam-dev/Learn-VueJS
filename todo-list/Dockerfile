FROM ubuntu:22.04

WORKDIR /app

COPY package*.json ./

RUN pnpm run build

EXPOSE 5173