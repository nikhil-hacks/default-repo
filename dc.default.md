# docker-compose.yml
services:
  nginx:
    image: nginx:latest
    container_name: my-nginx
    ports:
      - "8080:80"
    volumes:
      - ./index.html:/usr/share/nginx/html/index.html
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    restart: always


    #default.conf

    server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
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
