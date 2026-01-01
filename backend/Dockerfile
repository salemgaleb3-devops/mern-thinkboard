# Use official Node image
FROM node:20-alpine

# Create app directory
WORKDIR /app

# Install backend deps
COPY package*.json ./
RUN npm install

# Copy all backend code
COPY . . .

# Make port available
EXPOSE 5000

# Start server (use node or build command depending on your project)
CMD ["npm", "start"]

