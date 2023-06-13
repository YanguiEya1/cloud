# Stage 1: Build React app
FROM node:14-alpine AS build

WORKDIR /app

# add '/app/node_modules/.bin' to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install application dependencies
COPY package*.json ./
RUN npm install

# copy app files
COPY . .
RUN npm run build

# Stage 2: Serve the built app using NGINX
FROM nginx:alpine

# Copy the built app from the previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 (the default port for NGINX)
EXPOSE 80

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
