# Base image
FROM ubuntu:20.04

# Update and install Apache2
RUN apt-get update && apt-get install -y apache2

# Expose port 80
EXPOSE 80

# Start Apache2 service
CMD ["apachectl", "-D", "FOREGROUND"]
