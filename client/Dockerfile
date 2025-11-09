# Build stage
FROM node:16-alpine as build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy source code
COPY . .

# Build the React app - THIS MUST SUCCEED
RUN npm run build

# Verify build was created
RUN ls -la build/ || echo "Build failed!"

# Production stage
FROM node:16-alpine

WORKDIR /app

# Install serve globally
RUN npm install -g serve

# Copy built app from build stage - THIS MUST WORK
COPY --from=build /app/build ./build

# Verify build files are copied
RUN ls -la build/ || echo "No build files copied!"

EXPOSE 3000

CMD ["serve", "-s", "build", "-l", "3000"]