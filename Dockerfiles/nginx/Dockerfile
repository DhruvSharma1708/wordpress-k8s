FROM openresty/openresty:alpine

RUN apk update && \
    apk add --no-cache build-base curl pcre-dev zlib-dev && \
    cd /tmp && \
    curl -R -O http://nginx.org/download/nginx-1.19.10.tar.gz && \
    tar zxf nginx-1.19.10.tar.gz && \
    cd nginx-1.19.10 && \
    ./configure --prefix=/opt/openresty \
                --with-pcre-jit \
                --with-ipv6 \
                --without-http_redis2_module \
                --with-http_iconv_module \
                --with-http_postgres_module \
                -j8 && \
    make && make install

COPY nginx.conf /usr/local/openresty/nginx/conf/nginx.conf
COPY lua /usr/local/openresty/nginx/lua
