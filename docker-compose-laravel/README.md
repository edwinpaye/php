# Entorno de trabajo laravel con docker-compose
El entorno compondra php, laravel, nodejs, nginx y mysql.
Cada servicio estara en un contenedor Docker y usaremos docker-compose para trabajar con el conjunto de servicios.

## Usage

El entorno trabajara en la ruta especificada en el docker-compose.yml en este caso el archio /src paralelo al archivo /nginx, puedes usar otros archivos y especificarlos en el docker-compose.

volumes:
      - ./src:/var/www/html

Las usaremos el directorio /nginx para el archivo default.con, configuraciones del servidor nginx.

En la terinal nos dirigimos al directorio donde contenga el archio docker y ejecutaremos: `docker-compose up -d --build`. Si abrimos el navegador y nos dirigimos a: [http://localhost:8080](http://localhost:8080) estara corriendo el servidor.

**New:** Three new containers have been added that handle Composer, NPM, and Artisan commands without having to have these platforms installed on your local computer. Use the following command templates from your project root, modifiying them to fit your particular use case:

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

Containers created and their ports (if used) are as follows:

- **nginx** - `:8080`
- **mysql** - `:3306`
- **php** - `:9000`
- **npm**
- **composer**
- **artisan**

## Persistent MySQL Storage

By default, whenever you bring down the docker-compose network, your MySQL data will be removed after the containers are destroyed. If you would like to have persistent data that remains after bringing containers down and back up, do the following:

1. Create a `mysql` folder in the project root, alongside the `nginx` and `src` folders.
2. Under the mysql service in your `docker-compose.yml` file, add the following lines:

```
volumes:
  - ./mysql:/var/lib/mysql
```