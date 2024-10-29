# Preparativos

**Crear la carpeta donde almacenar el docker-compose.yaml**   
<code>mkdir prestashop</code>      
<code>cd prestashop</code>   

**Crear el archivo docker-compose.yaml**   
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

# Instalación
**Lanzar el docker compose**   
<code>docker compose up -d</code>

**Comprobar que se crearon los contenedores y están en ejecución**   
<code>docker ps -a</code>   

~~~
enrique@damenrique:~$ docker ps -a
CONTAINER ID   IMAGE                          COMMAND                  CREATED        STATUS                      PORTS                                     NAMES
7d88bdc2e783   prestashop/prestashop:latest   "docker-php-entrypoi…"   21 hours ago   Up 31 minutes               0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   containerPrestaShop
816b9a025d02   mysql:latest                   "docker-entrypoint.s…"   21 hours ago   Up 38 minutes               3306/tcp, 33060/tcp                       containerMySql
~~~

# Configuración
**Entrar a la página desde el navegador** *\<ip\>:\<puerto\>*   

![image](https://github.com/user-attachments/assets/94dbaae8-21b5-4427-9f72-757780c33fe9)

*Poner como dirección del servidor el nombre del container de la base de datos*   
![image](https://github.com/user-attachments/assets/ca691c59-e35e-4f88-b506-2981194b0f30)

**Comenzará la instalación**   

![image](https://github.com/user-attachments/assets/a20e1326-28ac-4ddb-bacf-18a5cd707df1)
![image](https://github.com/user-attachments/assets/891f751d-1285-4586-86a1-f414364a98aa)

**Una vez terminado ya podemos acceder a la tienda**   

![image](https://github.com/user-attachments/assets/9c5a0d80-f490-4396-a849-1495ba0addea)

**Para acceder a la página de administración:**   
Entrar en el container de prestashop   
<code>docker exec -it containerPrestashop /bin/bash</code>   

Eliminar la carpeta *install* localizada en /var/www/html   
<code>rm -r install/*</code>     
<code>rmdir install/</code>     

Cambiar el nombre de la carpeta *admin* localizada en /var/www/html   
<code>mv admin/ admin1234/</code>   

Una vez hecho esto, accedemos a la página de admin con *\<ip\>:<\puerto\>/admin1234   

![image](https://github.com/user-attachments/assets/cfaeeda5-0c00-40df-b89b-f4d8e22cf2c6)



