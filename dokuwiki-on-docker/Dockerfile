# Utiliza la imagen base de Ubuntu
FROM ubuntu:latest

# Actualiza el sistema y luego instala Apache2, PHP y herramientas adicionales
RUN apt-get update 
RUN apt-get install apache2 -y
# En esta parte se establece la zona horaria para evitar que se pida en el intall de php 
RUN ln -snf /usr/share/zoneinfo/UTC /etc/localtime && echo UTC > /etc/timezone
RUN apt-get install php -y

# Descarga la aplicación dokuwiki desde la web y la extrae en la carpeta raíz de Apache
RUN apt-get install wget -y
RUN wget -O /var/www/html/dokuwiki-stable.tgz https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
RUN tar -xzf /var/www/html/dokuwiki-stable.tgz -C /var/www/html/
RUN mv /var/www/html/dokuwiki*/ /var/www/html/dokuwiki
RUN rm /var/www/html/dokuwiki-stable.tgz
RUN rm /var/www/html/index.html

# Ajusta los permisos
RUN chown -R www-data:www-data /var/www/html/dokuwiki

# Inicia el apache
RUN update-rc.d apache2 enable
RUN service apache2 start
