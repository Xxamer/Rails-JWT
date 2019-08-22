# Rails-JWT

Esta es una API desarrollada en rails para probar la autenticación basada en token. Contiene login y registro de usuario aparte de "posts" para comprobar dicha autorización.


## Creación de los ficheros necesarios

Los ficheros se han creado usando la orden `` rails g scaffold User name surname password_digest `` para los usuarios y `` rails g scaffold Posts name description `` para los posts

![Imgur](https://i.imgur.com/vbB5YO7.png)


![Imgur](https://i.imgur.com/bGDM9TI.png)

## Instalación de gemas 

Las gemas necesarias las instalaremos en el fichero `` Gemfile ``, estas gemas son `` bcrypt ``, ``JWT`` y ``simple_command `` despues de esto ejecutamos `` bundle install `` 

![Imgur](https://i.imgur.com/OQ2vuLl.png)

## Pasos previos
En el fichero `` user.rb `` añadimos la línea ``has_secure_password `` para encriptar las contraseñas

![Imgur](https://i.imgur.com/aJ7YtuG.png)

En el fichero `` users_controller.rb `` en `` def user_params `` cambiamos los parámetros para añadir la contraseña y la confirmación de la contraseña en vez de "password_digest"

### Antes

![Imgur](https://i.imgur.com/mJtD4OH.png)

### Después
![Imgur](https://i.imgur.com/86NyCTA.png)