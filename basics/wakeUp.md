# ☀️ levantar un contenedor ☀️

## desde terminal 🖥

```Shell
docker run --name tu-contendorcito -p 80:80 -d tu-imagencita
```
también hay atajos que podemos hacer a la hora de lanzar un comando como combinar banderas

```Shell
docker run -dp 80:80 tu-imagencita
```

## usando  `docker build`

el comando `build` de docker hace uso de un archivo llamado Dockerfile ,sin extensiones.

dentro del archivo de Dockerfile tenemos que indicar la configuración de nuestro contenedor

```Dockerfile
# en from indicamos la imagen qeu queremos usar
FROM node:10-alpine 
# el directorio de trabajo desde donde estamos usando o vamos a usar archivos
WORKDIR /app
# aquí indicamos la ruta que queremos copiar y donde la queremos copiar
# con el punto indicamos que es la carpeta desde donde estamos lanzando el comando
COPY . .
# RUN nos permite ejecutar comandos al levantar el contenedor
RUN yarn install --production
# CMD se ejecutara después de RUN y son los comandos que vamos a lanzar
# en este caso ejecutamos el script index.js a través de node
CMD ["node", "/app/src/index.js"]

```

ya tenemos el archivo que dará forma a nuestra nueva imagen.
Vamos a crearla

```Shell

docker build -t getting-started .
# atención al punto que hace referencia a la ruta desde donde se lanza el comando
# que básicamente es donde va a buscar el Dockerfile para realizar el build

```
Ahora vamos a levantar nuestra imagen como vimos anteriormente

```Shell
# buscamos la ultima imagen que hemos creado
docker ps -a

# lanzamos un docker run con esa imagen

docker run -dp 9000:9000 getting-started
# por defecto al lanzar el comando asi nos va a crear un contenedor con un nombre random

# si todo va bien tenemos el contendor corriendo

```

esta es una forma muy util de por ejemplo encapsular el funcionamiento de distintas aplicaciones desde back a front o microservicios

#### hacemos un cambio??

Vamos a suponer que realizamos algún cambio en nuestro proyecto. Por ejemplo una librería nueva o cualquier cosa que se te ocurra.

supongamos que ya hemos hecho los cambios y hemos guardado hecho el commit de turno, etc.

Volvemos a construir la imagen con el comando `build`

```Shell
docker build -t getting-started2 .
#puedes poner el nombre que quieras incluso el mismo aunque previamente tendrás que borrar el anterior
```
volvemos a ejecutar `run` con la nueva imagen y comprobamos que el servicio esta bien


### tips

es posible que haciendo el proceso te suelte un fallo del palo

`docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell (bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.` 

simplemente nos esta indicando que el puerto actualmente esta en uso tiene 2 soluciones:

1. la fácil cambiar el puerto que has destinado para el contenedor del lado de tu maquina
```Shell
# con fallo
docker run -dp 80:80 super-app

# cambiamos el puerto y fuera el fallo
docker run -dp 8074:80 super-app

2. tirar abajo el servicio de nuestro equipo, salvo que sepas muy bien lo que vas a tocar no lo hagas, o bueno hazlo 😈



