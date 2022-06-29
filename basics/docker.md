# Docker

## que es docker

### primero para dummys 🥴

A grandes rasgos docker es una forma de virtualizar servicios de forma fácil.

#### [⬇️vamos al lio⬇️](#go-deeper-🧑🏽‍💻)

### expliquemos un poco 📝

imaginemos que necesitamos una base de datos por ejemplo mongoDB. Sabemos que mongoDB es una servicio de base de datos que deberíamos instalar en nuestro ordenador, configurar el servicio y por ultimo usarlo de la forma en la que mas nos convenga.

Ahora bien es posible que necesites cambiar de entorno mas de una vez y que tengas que repetir este proceso en mas de una ocasión.

Y si pudieras tener solo mongo y si pudieras hacerlo independiente del SO.

Esta es la solución que nos trae docker un ejemplo con mongo

```shell
docker run --name my-mongo-db -p 27017:27017 -d mongo:5.0
```

arriba simplemente estamos indicando que
1. `docker`vamos a usar docker
2. `run` vamos a lanzar el siguiente contenedor
3. `--name` el nombre de nuestro contenedor
4. `-p` mapeamos el puerto del contenedor y por el cual vamos a acceder desde nuestro equipo
  - el primer dígito indica el puerto de nuestro ordenador y el segundo el puerto que tendrá docker

5. `-d` la imagen que vamos a usar, ademas si continuamos el nombre de la imagen con : indicamos la version de la imagen

Claro que para hacer todo esto debemos instalar docker

# [👉 Go to docker instalación 👉](https://docs.docker.com/get-started/)  

## Lo básico 🥺

como viste en el ejemplo de arriba por ***terminal*** solo tenemos que invocar a docker y luego a través de una serie de banderas realizar la configuración

veamos un par de comandos de docker

### run

con este comando levantamos un contenedor

- si no tenemos la imagen del contenedor la descargara
- si le damos el mismo nombre de otro contenedor nos dará fallo

### start

hemos apagado el ordenador y vamos a usar nuestro flamante servicio de mongo, pero cuando estamos en el lio resulta que la base de datos no va ERR CON REFUSED  y palabrotas varias.

No pasa nada simplemente docker no esta activo

podemos usar el comando `start` para lanzar nuestro contenedor

```shell
docker start <nombre-contenedor>

o

docker start <identificador>

```

### ps

con este comando podemos ver un listado de los contenedores que tenemos actualmente

```shell
docker ps 
# este comando nos muestra los contenedores que están corriendo

docker ps -a
# con la bandera -a nos mostrara todos los contenedores incluyendo los que están abajo
```
# Go deeper 🧑🏽‍💻

### [levantar un contenedor](./wakeUp.md)
### [otros comandos](moreComands.md)



