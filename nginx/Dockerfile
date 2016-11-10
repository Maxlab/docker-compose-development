FROM nginx:1.10.1

MAINTAINER Stepanov Nikolai <nstepanovdev@gmail.com>

RUN mkdir -p /tmp/nginx && mkdir -p /tmp/nginx/cache && mkdir -p /tmp/nginx/cache

CMD "/bin/bash"

RUN groupadd -g 1000 app && \
    useradd -g 1000 -u 1000 -d /data -s /bin/bash app

COPY nginx /etc/nginx

WORKDIR /data
CMD ["nginx"]


