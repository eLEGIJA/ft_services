FROM alpine:latest
RUN apk update && apk upgrade && apk add supervisor && apk add openssl && apk add openrc \
	&& apk add openssh && apk add nginx && adduser -D -g 'www' www

RUN echo "www:password" | chpasswd
RUN mkdir /www
RUN chown -R www:www /var/lib/nginx
RUN chown -R www:www /www

COPY nginx.conf /etc/nginx/
COPY index.html /www/
COPY start_nginx.sh .
COPY supervisor.conf /etc/supervisord.conf

RUN openssl req \
		-newkey rsa:2048 -nodes -keyout local_host.key \
		-x509 -days 365 -out local_host.crt \
		-subj "/C=RU/ST=Moscow/L=Moscow/O=21school/OU=21/CN=msafflow"

CMD sh start_nginx.sh

EXPOSE 80 443