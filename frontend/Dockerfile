FROM centos:7

LABEL APP="Studentapp_frontend"
LABEL DevopsEngg="devops_vighnesh"

RUN apt install httpd -y
COPY index.html /var/www/html/index.html

EXPOSE 80
CMD httpd -DFOREGROUND 