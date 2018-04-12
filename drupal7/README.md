# Usage

docker-compose.yml

```yaml
version: '2'
services:
  apache:
    image: drupal:7
    volumes:
      - .:/var/www/html
    expose:
      - "80"
    links:
      - mariadb
    depends_on:
      - mariadb
  console:
    image: touch4it/drupal-drush:7
    volumes:
      - .:/app
    links:
      - mariadb
    depends_on:
      - mariadb
  mariadb:
    image: mariadb:10.0.33
      - ./mysql:/var/lib/mysql
    expose:
      - "3306"
```

```bash
docker-compose up -d
docker exec -it drupal-drush_console_1 drush
docker exec -it drupal-drush_console_1 drush cache-clear all
docker-compose down
```
