# Use the official Node.js 18 slim image as the base image
FROM node:18-slim

# Set the working directory in the container
WORKDIR /app

RUN apt-get update -y && apt-get install -y openssl

# Copy the package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install the Node.js dependencies
RUN npm install

# Generate the Prisma client
RUN npx prisma generate

# Copy the entire project directory to the working directory
COPY . .

# Expose port 3000
EXPOSE 3000

# Start the Next.js app
CMD ["npm", "run", "dev"]
