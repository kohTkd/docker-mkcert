# docker-mkcert
A Docker container for https enabled nginx reverse proxy.

## Setup

```bash
cd /path/to/directory
git clone https://github.com/kohTkd/docker-mkcert.git
cd ./docker-mkcert
docker-compose up -d
```

## Install rootCA

1. Access http://localhost/rootCA.pem and download it.
2. Add rootCA.pem to trusted root certifications on your computer.
    - If you use macOS, open and trust it on keychain.

## Access localhost via HTTPS

1. Start your backend application, such as Ruby on Rails, PHP, and so on.
1. Overwrite docker-compose.yml environment for your backend application.
1. If you need, modify nginx.conf as you like.
1. Access https://localhost, then you can access your application over HTTPS!
