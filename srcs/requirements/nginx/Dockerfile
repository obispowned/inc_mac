FROM debian:buster

    #Actualizacion e instalacion de utilidades
RUN apt-get update && apt-get upgrade -y
RUN apt-get install apt-utils -y

    #Instalacion Nginx
RUN apt-get install -y nginx

    #Instalacion de protocoloSSL, permiso y acceso
RUN apt-get install -y openssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \ 
	-subj "/C=SP/ST=Spain/L=Madrid/O=42Madrid/CN=agutierr.42.fr" \
	-keyout /etc/ssl/private/agutierr.key -out /etc/ssl/certs/agutierr.crt

RUN mkdir -p /var/www/agutierr/html
RUN chown -R www-data:www-data /var/www/agutierr/html
RUN chmod -R 775 /var/www/agutierr

    #Agregar configuracion
COPY conf/nginx.conf /etc/nginx/
COPY agutierr /etc/nginx/sites-available/
COPY index.html /var/www/agutierr/html/

RUN chown -R www-data:www-data /var/www/agutierr/html
#RUN rm /etc/nginx/sites-enabled/*
#RUN ln -sf /etc/nginx/sites-available/agutierr /etc/nginx/sites-enabled


EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
