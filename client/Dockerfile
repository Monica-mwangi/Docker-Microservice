# Build stage
FROM node:16-alpine as build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci

# Install serve globally
RUN npm install serve

# Copy source code
COPY . .

# Build the React app
RUN npm run build

# Production stage
FROM node:16-alpine

WORKDIR /app



# Copy built app from build stage
COPY --from=build /app/build ./build

# Expose port
EXPOSE 3000

# Serve the app
CMD ["serve", "-s", "build", "-l", "3000"]
