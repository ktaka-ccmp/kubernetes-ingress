FROM nginx:1.11.1

# forward nginx access and error logs to stdout and stderr of the ingress
# controller process
RUN ln -sf /proc/1/fd/1 /var/log/nginx/access.log \
	&& ln -sf /proc/1/fd/2 /var/log/nginx/error.log

COPY nginx-ingress nginx/ingress.tmpl nginx/nginx.conf.tmpl /

RUN rm /etc/nginx/conf.d/*
RUN apt-get update ; apt-get install wget curl -y
RUN wget http://nginx.org/keys/nginx_signing.key -O - |apt-key add -
RUN apt-get update && apt-get install net-tools less tcpdump jq -y

ENTRYPOINT ["/nginx-ingress"]

