# Compose 🎼

## que es?

### Dummie time 🐣

Es una forma de crear, conectar y levantar nuestros contenedores.
Es un archivo con una serie de pasos para construir nuestra solución.

### un poco mas de materia

Compose nos da la capacidad de establecer de forma sencilla mediante una lenguaje a mas alto nivel como queremos `componer` nuestro contenedor de contenedores.

para ello vamos a hacer uso de un archivo el `docker-compose.yml`

vamos a ver un ejemplo 

```yml
version: "3.8"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

vamos a estudiarlo un poquito.

## version

nos indica la version de esquema para nuestro archivo

## services

los contenedores que vamos a crear

como vemos tenemos 2
- app
- mysql

una cosa que mola de hacerlo con compose es que automaticamente el nombre que le demos aqui sera el alias definido en el `network`

## image

la imagen que usaremos en ese volumen

## commands

los comandos que lanzaremos una vez levantado el contenedor

## ports

el mapeo de los puertos

## working_dir

el directorio de trabajo

## volume

el mapeo de donde se va a montar la ruta en el contenedor

## enviroment

las variables de entorno

## volumes

los volumenes que vamos a crear para esta compose