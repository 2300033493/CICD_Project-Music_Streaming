# ---------- Build stage ----------
FROM node:20-alpine AS builder

WORKDIR /app

RUN apk add --no-cache git

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

# ---------- Run stage ----------
FROM nginx:alpine

# Copy the build output from the 'builder' stage to the Nginx web root
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy the nginx.conf file from the project's root to the Nginx configuration directory
# This command is the key to solving your issue.
# It places the config file in a directory that Nginx is configured to include.
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
