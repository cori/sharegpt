# Use the official Node.js 18 slim image as the base image
ARG NODE_CONTAINER_VERSION=18-slim
FROM node:${NODE_CONTAINER_VERSION} as build

# Set the working directory in the container
WORKDIR /app

RUN apt-get update -y && apt-get install -y openssl

# Copy the package.json and yarn.lock files to the working directory
COPY package.json yarn.lock prisma/schema.prisma ./

# Install the Node.js dependencies
RUN yarn install --frozen-lockfile --production

# Generate the Prisma client
RUN npx prisma generate --schema=schema.prisma

# Copy the entire project directory to the working directory
COPY . .

# Build the application
RUN yarn build

FROM node:${NODE_CONTAINER_VERSION}

WORKDIR /app

COPY --from=build /app .

# Expose port 3000
EXPOSE 3000

# Start the Next.js app
CMD ["yarn", "start"]
