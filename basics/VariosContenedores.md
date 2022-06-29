# multiContainers

vale mas o menos ya vamos viendo como mola esto de los contenedores.

y si ahora te digo que puedes tener cada una de tus aplicaciones corriendo en contenedores diferentes y que estas pueden estar comunicadas entre si

![mas matao!](../assets/img/mind-blown.gif)

## Network

Necesitamos crear una relacion entre ambos contenedores para que se comuniquen

```Shell
docker network create <nombre-de-la-red>

#ejemplo real
docker network create todo-app

```

ahora vamos a crearnos un contenedor de mysql como servicio de base de datos

```Shell
docker run -d \
    --network todo-app --network-alias mysql \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:5.7

```

***Repasemos un poco:***
- --network --> indicamos la red/network que vamos a usar
- --network-alias --> el nombre que va a tomar el contenedor dentro de la network
- -v --> el volumen [mas info](./volumenes.md)
- -e --> variables de entorno

> siempre es recomendable comprobar los contenedores y que estos esten ok

```Shell
docker exec -it <mysql-container-id> mysql -p
# te pedira el pass , previamente puesto en la variable de entorno
mysql> SHOW DATABASES;
```

## conectar con el otro contenedor

pues casi que simplemente es indicarle la `network` y el contenedor `alias`

hay que tener en cuenta que para crear el siguiente contenedor la aplicacion tambien va a usar las variables de entorno. Esto dependera de como lo tengas configurado.

veamos el ejemplo:

```Shell
docker run -dp 3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:12-alpine \
  sh -c "yarn install && yarn run dev"

```

- como vemos establecemos la network igual que el otro contenedor
- la variable MYSQL_HOST, hace referencia al contenedor con el `alias` mysql
- el resto de variables se configuran como se hacen usualmente
- por ultimo se instalan las dependencias y se  ejecuta en modo desarrollo

Solo queda probar las funcionalidades que hagan uso de la base de datos



