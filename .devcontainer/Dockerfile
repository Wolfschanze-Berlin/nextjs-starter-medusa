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
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Enable Corepack for Yarn 3.x support
RUN corepack enable

# Create a non-root user (node user already exists in the base image)
# Just ensure proper ownership of workspace
RUN mkdir -p /workspace && chown -R node:node /workspace

# Set the working directory
WORKDIR /workspace

# Switch to non-root user
USER node

# Set environment variables
ENV NODE_ENV=development
ENV SHELL=/bin/bash

# Verify installations
RUN node --version && npm --version && corepack --version