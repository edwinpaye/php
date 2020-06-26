# Entorno de trabajo laravel con docker-compose

El entorno compondra php, laravel, nodejs, nginx y mysql.
Cada servicio estara en un contenedor Docker y usaremos docker-compose para trabajar con el conjunto de servicios.

## Como usar el entorno de trabajo

El entorno trabajara en la ruta especificada en el docker-compose.yml en este caso el archio /src paralelo al archivo /nginx, puedes usar otros archivos y especificarlos en el docker-compose.yml

volumes:
      - ./src:/var/www/html

Las usaremos el directorio /nginx para el archivo default.con, configuraciones del servidor nginx.

En la terinal nos dirigimos al directorio donde contenga el archio docker y ejecutaremos: `docker-compose up -d --build`. Si abrimos el navegador y nos dirigimos a: [http://localhost:8080](http://localhost:8080) estara corriendo el servidor.

## Como usar los servicios como los manejadores de dependencia npm, composer, etc

Ejecutaremos los comandos con la herramienta de docker-compose para levantar el servicio y que una vez terminada la tarea asignada, este servicio se eliminara del segundo plano.

`docker-compose run --rm nombreDelContenedor comandoDeEjecucion`

Por ejemplo: 

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

En el caso que querramos ejecutar comandos dentro del contenedor

`docker-compose run --rm nombreDelContenedor nombreDelServicio comandoDeEjecucion`

- `docker-compose run --rm composer composer create laravel/laravel project .`
- `docker-compose run --rm npm npm install`
- `docker-compose run --rm artisan artisan make:controller NewController --` 

Los puertos donde se exponene los servicios de los contenedores docker son:

- nginc - :8080
- mysql - :3306
- php - :9000
- npm - puerto default asignado por docker
- composer - puerto default asignado por docker
- artisan - puerto default asignado por docker

## Persistent MySQL Storage

Para la persistencia de MySQL en un directorio se consigue de la siguiente forma:

1. Crea un directorio mysql en el directorio que aloja este README junto con los otro directorios de /nginx y /src
2. Descomenta las siguientes lineas del archivo docker-compose.yml

volumes:
  - ./mysql:/var/lib/mysql