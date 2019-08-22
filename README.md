# Rails-JWT

Esta es una API desarrollada en rails para probar la autenticación basada en token. Contiene login y registro de usuario aparte de "posts" para comprobar dicha autorización.


## Creación de los ficheros necesarios

Los ficheros se han creado usando la orden `` rails g scaffold User name surname password_digest `` para los usuarios y `` rails g scaffold Posts name description `` para los posts.

![Imgur](https://i.imgur.com/vbB5YO7.png)


![Imgur](https://i.imgur.com/bGDM9TI.png)

## Instalación de gemas 

Las gemas necesarias las instalaremos en el fichero `` Gemfile ``, estas gemas son `` bcrypt ``, ``JWT`` y ``simple_command `` despues de esto ejecutamos `` bundle install ``.

![Imgur](https://i.imgur.com/OQ2vuLl.png)

## Pasos previos
En el fichero `` user.rb `` añadimos la línea ``has_secure_password `` para encriptar las contraseñas.

![Imgur](https://i.imgur.com/aJ7YtuG.png)

En el fichero `` users_controller.rb `` en `` def user_params `` cambiamos los parámetros para añadir la contraseña y la confirmación de la contraseña en vez de "password_digest".

### Antes

![Imgur](https://i.imgur.com/mJtD4OH.png)

### Después
![Imgur](https://i.imgur.com/86NyCTA.png)

En el fichero ``config/application.rb `` añadimos la línea ``config.autoload_path << Rails.root.jon('lib')`` para cargar los ficheros de configuración que posteriormente añadiremos a la carpeta lib.
![Imgur](https://i.imgur.com/9y7fO42.png)

## Archivos de configuración 

Dentro de la carpeta ``app`` crearemos la carpeta ``commands`` y dentro el fichero ``authenticate_user.rb``.

![Imgur](https://i.imgur.com/WPbSH01.png)

Dentro de la misma carpeta ``commands`` añadiremos otro fichero que será llamado ``authorize_api_request.rb`` que revisará que el token sea valido

![Imgur](https://i.imgur.com/UN7ChNF.png)

En la carpeta `` lib `` crearemos el archivo `` json_web_token.rb`` que contendrá los métodos para codificar y decodificar el token.

![Imgur](https://i.imgur.com/p09qqP6.png)

En la carpeta ``controllers `` añadiremos un fichero llamado ``authentication_controller.rb `` que en caso de no tener autorización rechazará la petición con el estado de no permitido.
![Imgur](https://i.imgur.com/jvaJ2hU.png)

En el fichero ``application_controller.rb`` añadiremos el método "authenticate_request" que hará que antes de ejecutar cualquier petición a la API se compruebe la autenticación.

![Imgur](https://i.imgur.com/tzmrykc.png)

Para permitir la creación de usuarios añadiremos que la autenticación solo sea necesaria en las peticiones de actualizacion y destrucción dentro del fichero ``application_controller.rb`` 
![Imgur](https://i.imgur.com/x7xkzsH.png)


Cómo último paso añadiremos en el fichero ``routes.rb`` la ruta para el controlador de la autenticación

![Imgur](https://i.imgur.com/QAKpWpx.png)

## Comprobando el funcionamiento con Postman

Si intentamos acceder sin autenticación aparecerá el error 401 unauthorized
![Imgur](https://i.imgur.com/6X7fYWv.png)

Crearemos un usuario de prueba con una contraseña y veremos que nos permite realizarlo ya que añadimos la línea de no realizar autenticación en las peticiones de creación 
![Imgur](https://i.imgur.com/eMnVTvw.png)

Y si realizamos una petición al end-point de autenticación con el usuario y la contraseña que pusimos a la hora de registrar el usuario nos devolverá el token de ese usuario

![Imgur](https://i.imgur.com/BahGznC.png)