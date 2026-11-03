# docker-compose.yml
services:
  nginx:
    image: nginx:latest
    container_name: nginx-server
    ports:
      - "8080:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
      - ./web1.html:/usr/share/nginx/html/web1.html
      - ./web2.html:/usr/share/nginx/html/web2.html
    restart: always


    #default.conf
  server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index web1.html;
    }

    location /web1 {
        root /usr/share/nginx/html;
        index web1.html;
    }

    location /web2 {
        root /usr/share/nginx/html;
        index web2.html;
    }
}


# Start containers
docker compose up -d

# Check running containers
docker compose ps

# View logs
docker compose logs

# Stop containers
docker compose down
