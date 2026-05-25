FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./
EXPOSE 8080

FROM base AS development
RUN npm install
COPY src/ ./src/
CMD ["npm", "run", "dev"]

FROM base AS build
RUN npm ci --omit=dev

FROM node:20-alpine AS production
WORKDIR /app

COPY --from=build /app/node_modules ./node_modules
COPY package*.json ./
COPY src/ ./src/

EXPOSE 8080
CMD ["node", "src/index.js"]