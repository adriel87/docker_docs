# Volúmenes

O como hacer espacios para guardar información de forma permanente y que pueda ser usada por nuestro contenedores 📦

Es relativamente habitual que hagamos modificaciones sobre un contenedor y vuelvas a crear la imagen y pufff igual has creado algo que querías mantener.

pues para eso están los volúmenes

por ejemplo creamos un volumen que un nuevo contenedor

## creando un nuevo volumen y usándolo

```Shell
# creamos el volumen
docker volume create base-de-datitos

# usamos a nuestro amigo run, pero esta vez indicamos el volumen  que usamos y donde lo montamos
docker run -dp 3000:3000 -v base-de-datitos:/etc/bbdd getting-started
```

ahora podemos hacer gestiones con nuestra base de datos, ten encuentra que lo que hace el volumen que hemos creado es copiar todo lo que pase dentro de la dirección proporcionada.

Me refiero a  que tu base de datos o mejor dicho la información de la misma esta montada en otro lugar. Tienes que tener ojo con eso

## comprobando que funciona

ahora vamos a ver si esto `furula`

```Shell
# listamos nuestros contenedores
docker ps

# cogemos el id o el name del  contenedor que hicimos previamente y lo borramos vilmente
# con la bandera -f forzamos que el contenedor pare y lo borramos, de hay viene vilmente 
docker rm -f <container or name id>

```

ya nos cargamos el contenedor ☠️

vamos levantar uno nuevo y volvemos a usar el volumen anterior

```Shell
docker run -dp 3000:3000 -v base-de-datitos:/etc/bbdd getting-started
```

ahora podremos comprobar si la base de datos tiene los datos que previamente habíamos creado/modificado


