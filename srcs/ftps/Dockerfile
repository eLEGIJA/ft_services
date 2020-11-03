FROM alpine:latest

RUN	apk update upgrade
RUN	apk add openrc openssl vsftpd
RUN printf "msafflow\nmsafflow\n" | adduser msafflow -s /bin/false -h /msafflow
RUN	chown msafflow:msafflow /msafflow

COPY vsftpd.conf /etc/vsftpd/vsftpd.conf
COPY start_vsftpd.sh .

RUN openssl req \
		-newkey rsa:2048 \
		-nodes \
		-keyout /etc/vsftpd.key \
		-x509 \
		-days 365 \
		-out /etc/vsftpd.crt \
		-subj "/C=RU/ST=Moscow/L=Moscow/O=21school/OU=21/CN=msafflow"

EXPOSE 21 20 21000

ENTRYPOINT [ "sh", "start_vsftpd.sh" ]