# docker-mkcert
A Docker container for https enabled nginx reverse proxy.

## Setup

```bash
cd /path/to/directory
git clone https://github.com/kohTkd/docker-mkcert.git
cd ./docker-mkcert
docker-compose build
```

## Access localhost via HTTPS

1. Start your backend application, such as Ruby on Rails, PHP, and so on.
2. Overwrite docker-compose.yml environment for your backend application.
3. If you need, modify nginx.conf as you like.
4. Run `docker-compose up -d`
5. Access http://localhost/rootCA.pem and download it.
6. Add rootCA.pem to trusted root certifications on your computer.
    - If you use macOS, open and trust it on keychain.
7. Access https://localhost, then you can access your application over HTTPS!
