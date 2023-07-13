# Base image
FROM ubuntu:20.04

# Update and install Nginx
RUN apt-get update && apt-get install -y nginx

# Expose port 80
EXPOSE 80

# Start Nginx service
CMD ["nginx", "-g", "daemon off;"]