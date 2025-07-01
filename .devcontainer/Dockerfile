# Use Node.js 20 LTS as base image
FROM node:20-bullseye

# Install additional system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    wget \
    unzip \
    vim \
    nano \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

# Enable Corepack for Yarn 3.x support
RUN corepack enable

# Set the working directory
WORKDIR /workspace

# Create a non-root user
RUN groupadd --gid 1000 node \
    && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

# Set up proper permissions
RUN chown -R node:node /workspace

# Switch to non-root user
USER node

# Set environment variables
ENV NODE_ENV=development
ENV SHELL=/bin/bash