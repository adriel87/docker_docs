# Simular 

como podemos probar un contenedor en el que vamos ir realizando cambios a lo largo del dia. Y ademas ir realizando esos cambios en caliente y ver como afecta eso a la aplicación.

no seria genial tener un entorno de trabajo donde realizar todas las pruebas que queramos antes de hacer un build para luego pushear nuestra imagen??

## creando nuestro entorno

primero nos aseguramos que no tenemos ningún contenedor corriendo en el puerto donde vamos a trabajar

```Shell
docker ps
```

ahora nos colocamos donde tenemos el proyecto

`cd/el-path-de-tu-proyecto`

## toca docker

```Shell
# en linux
docker run -dp <port>:<port> -w /<carpeta del proyecto> -v "$(pwd):app" <imagen> sh -c "<tus comandos>"

# un ejemplo real
docker run -dp 3000:3000 \
    -w /app -v "$(pwd):/app" \
    node:12-alpine \
    sh -c "yarn install && yarn run dev"

```
expliquemos un poco las `banderas`

- -dp --> ya la conocemos mapeamos el puerto he indicamos la imagen
- -v --> volumen donde se  va a montar la app
- -w --> establece el directorio actual como directorio de trabajo
- sh -c --> indicamos que vamos a lanzar en la shell el comando

## ver que pasa en la maquina

```Shell
docker logs -f <id o nombre contenedor>
```

con esto podemos ver rápidamente el historial de logs del contenedor `CTRL + c` para salir

## ahora toca hacer los cambios

ahora dentro de nuestro proyecto los cambios

todo este tutorial se esta haciendo con la imagen de base de docker101 o el getting starter que proporciona docker.

Esta imagen tiene una aplicación que como dependencia de desarrollo tiene instalado el nodemon que básicamente resumiendo mucho va a realizar un refresh en la app cuando detecte algún cambio en nuestro código

Dicho esto puedes hacer el cambio y volver a probar el contenedor, es posible que si eres muy muy rápido te de algún tipo de error , simplemente espera un poco y vuelve a intentarlo.

## todo va de lujo

pues ahora puedes hacer tu build and push
