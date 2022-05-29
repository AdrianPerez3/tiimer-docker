# How to deploy the application

## 1.Como instalar la aplicacion

Iremos a mi repositorio: `https://github.com/AdrianPerez3/tiimer.git` y haremos un git clone.

Después instalaremos las librerias de composer con un `composer install`.

Finalemnte haremos un `yarn install` para instalar las librerias de js necesarias.

## 2.Inicializar la base de datos

En este caso se puede hacer de varias formas:

1. Inicializar contenedor con mysql y phpmyadmin.

Dentro del proyecto vais a encontrar un `docker-compose.yml`, contiene un contenedor de mysql y phpmyadmin.
Para inicializarlo simplemente es hacer un `docker-compose up -d`, despues entrar al `localhost:8081` poner usuario root y contraseña root
crear la bbdd ejemplo y importar la base de datos (se explica en el apartado 3).

2. Inicilaizar solo la bbdd:

```
version: "3.7"
# Define services/containers
services:
  # MySQL container
  mysql:
    # Use mysql:8.0.19 image
    image: mysql:5.7
    container_name: db-ejemplo
    # Connect to "my-network" network, as defined below
    networks:
      - my-network
    # Pass a list of environment variables to the container
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ejemplo
    volumes:
      - db-data:/var/lib/mysql
    ports:
      - "3306:3306"
      # Names our volume
volumes:
  my-db:
```

Gracias a esto crearéis un contendor con solo con mysql para utilizarla con DBeaver que es un software que actúa como 
una herramienta de base de datos universal o con mysql server.

Si queries llamar la base de datos de otra forma teneis que cambiarlo en el archivo de configuracion.
Debeis entrar al archivo `.env` y editar la siguente linea:

` DATABASE_URL="mysql://root:root@127.0.0.1:3306/ejemplo?serverVersion=5.7&charset=utf8mb4"
`

Donde en `/ejemplo?` que en mi caso la bbdd se llama ejemplo, vosotros tenies que ponder el nombre de la bbdd que habeis creado
en mysql

## 3 Como importar las bbdd:

Al hacer un clone habra un fichero llamado `tiimer.sql` simplemente tenieis que crear una base de datos
llamada ejemplo e importa la sql.

## 4 Inicializar el servidor

Hay dos formas posibles:

1. `symfony server:start`
Utilizareis este comando en el caso que tengais el cliente symfony instalado.

Podeis entrar al siguente enlace para descargarlo: 
`https://symfony.com/download`

2. `php -S localhost:8001`
La segunda opcion es hacer un simple php -S.


## 5 Usuario de ejemplos

Ya hay algunos usuarios creados que ya tienen datos:

1. rexinacho@hotmail.es , password: 123456
