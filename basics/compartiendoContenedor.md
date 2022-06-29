# Comparte

Usualmente trabajar con mas personas o simplemente quieras compartir algo que has creado dentro de tu flamante contenedor

1. deberías tener una cuenta en docker
2. tener un contenedor
3. subirlo a dockerhub

## logueate

desde la terminal con 
```Shell
docker login
# ahora te pedirá las credenciales
```

en la pagina de docker hub create un repositorio, usualmente usaras el mismo nombre que tendra la imagen.

ahora si ya te has logueado sin problemas pasemos al siguiente paso

## mira tus imágenes

```Shell
docker image ls
# listara las imágenes que tienes actualmente
```

es posible que no tengas tagueada/nombrada adecuadamente tu imagen vamos a ello

```Shell
docker tag <nombre/id de tu imagen> <nombredeusuariodocker>/<nombre del repo>

#un ejemplo algo mas real

docker tag settings-started paco/getting-started
```

por ultimo subirlo al repo

## pusheando

ya solo queda subir la imagen para futuros contenedores 

```Shell
#sigamos con paco
docker push paco/getting-started
```
como ves en este caso el comando que usamos es push como en git.

y el parámetro que le pasamos es el `tag` que hicimos en el paso previo.
