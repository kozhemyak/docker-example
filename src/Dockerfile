FROM nginx:alpine

LABEL Maintainer="Nikolay Kozhemyak <nkozhemyak@gmail.com>"

COPY site /usr/share/nginx/html/

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]