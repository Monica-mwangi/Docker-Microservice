# Build stage
FROM node:16-alpine as build

WORKDIR /app

# Copy package files first (better caching)
COPY package*.json ./

# Install dependencies
RUN npm ci --silent

# Copy source code
COPY . .

# Build the React app
RUN npm run build

# Verify build
RUN ls -la build/ && echo "✅ React build completed successfully!"

# Production stage
FROM node:16-alpine

WORKDIR /app

# Install serve globally
RUN npm install -g serve

# Copy ONLY the built app from build stage
COPY --from=build /app/build ./build

# Verify build files are copied
RUN echo "✅ Build files copied:" && ls -la build/

# Expose port
EXPOSE 3000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:3000/ || exit 1

# Serve the built app with SPA support
CMD ["serve", "-s", "build", "-l", "3000", "--single"]
