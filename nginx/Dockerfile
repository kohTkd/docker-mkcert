FROM nginx:alpine

ARG LISTEN=443
ARG DOMAIN='localhost'
ARG OTHER_DOMAINS='127.0.0.1'
ARG MKCERT_VERSION='v1.4.3'
# If you want to overwrite in docker-compose.yml, you need to escape such as "ENVSUBST_ARGS: '\\$$TARGET\\$$KEY_NAME'"
ARG ENVSUBST_ARGS='\$TARGET\$DOMAIN\$RESOLVER'

EXPOSE ${LISTEN}

RUN apk update && apk upgrade && \
    apk add --no-cache --update openssl && \
    rm -rf /var/cache/apk/* && \
    wget -O /usr/local/bin/mkcert https://github.com/FiloSottile/mkcert/releases/download/${MKCERT_VERSION}/mkcert-${MKCERT_VERSION}-linux-amd64 && \
    chmod +x /usr/local/bin/mkcert && \
    mkdir -p /etc/nginx/cert && \
    cd /etc/nginx/cert && \
    mkcert --install && \
    mkdir -p /usr/share/nginx/rootCA/${DOMAIN} && \
    cp `mkcert -CAROOT`/rootCA.pem /usr/share/nginx/rootCA/${DOMAIN}/rootCA.pem && \
    mkcert ${DOMAIN} ${OTHER_DOMAINS} && \
    find . -regex "\./${DOMAIN}\(+[0-9]\+\)\.pem" | xargs -i mv {} ${DOMAIN}.pem && \
    find . -regex "\./${DOMAIN}\(+[0-9]\+\)\-key\.pem" | xargs -i mv {} ${DOMAIN}-key.pem

COPY config/nginx.conf /etc/nginx/tmp/nginx.conf
ENV ENVSUBST_KEYS="${ENVSUBST_ARGS}"

CMD /bin/sh -c "envsubst '${ENVSUBST_KEYS}' < /etc/nginx/tmp/nginx.conf > /etc/nginx/nginx.conf && nginx -g 'daemon off;'"
