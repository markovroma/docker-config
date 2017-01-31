FROM nginx:latest
COPY ./ca.conf /etc/nginx/conf.d/
COPY ./ssl/public.pem /etc/ssl/public.pem
COPY ./ssl/private.pem /etc/ssl/private.pem
COPY ./include_ssl /etc/nginx
