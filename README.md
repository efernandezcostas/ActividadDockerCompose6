# 
<code>mkdir prestashop</code>
<code>cd prestashop</code>

<code>touch docker-compose.yaml</code>
<code>nano docker-compose.yaml</code>

~~~
name: tarea6

services:
  db:
    container_name: containerMySql
    image: mysql:latest
    restart: always
    environment:
      MYSQL_DATABASE: prestashopDB
      MYSQL_USER: enrique
      MYSQL_PASSWORD: admin
      MYSQL_ROOT_PASSWORD: admin 
    networks:
      - prestashop_network

  ps:
    container_name: containerPrestaShop
    image: prestashop/prestashop:latest
    depends_on: 
      - db
    ports:
      - 8080:80
    environment:
      DB_USER: enrique
      DB_PASSWD: admin
      DB_NAME: prestashopDB
    networks:
      - prestashop_network
networks:
  prestashop_network:
~~~

<code>docker compose up -d</code>
<code>docker ps -a</code>

![image](https://github.com/user-attachments/assets/94dbaae8-21b5-4427-9f72-757780c33fe9)

