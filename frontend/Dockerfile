# Build stage
FROM node:20-alpine AS build

WORKDIR /app

COPY frontend/package*.json ./
RUN npm install

COPY frontend ./
RUN npm run build

# Production stage (NO nginx)
FROM node:20-alpine

WORKDIR /app

# Install static file server
RUN npm install -g serve

# Copy build output
COPY --from=build /app/dist ./dist

EXPOSE 80

CMD ["serve", "-s", "dist", "-l", "80"]
