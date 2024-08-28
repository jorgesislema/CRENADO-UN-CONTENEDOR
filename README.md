
Guía para Crear un Contenedor de MongoDB en Linux


En esta guía, aprenderás a crear y configurar un contenedor de MongoDB en un entorno Linux utilizando Docker. Sigue los pasos a continuación para configurar tu entorno de desarrollo de manera eficiente.

Paso 1: Localizar el Directorio de Trabajo

Primero, debes ubicar el directorio donde almacenarás los archivos del contenedor. Utiliza los siguientes comandos en tu terminal:
# Muestra el directorio actual
>pwd
# Lista los archivos y carpetas
>ls
# Navega al directorio donde trabajará 
>cd /ruta/a/tu/carpeta/de/proyecto   s
____________________________________________________________________________________________________________________________________________________________________________________________
Paso 2: Crear el Archivo de Configuración docker-compose.yml

Crea un archivo llamado docker-compose.yml, que contendrá la configuración del contenedor:

>sudo touch docker-compose.yml
_________________________________________________________________________________________________________________________________________________________________________________________
Paso 3: Editar el Archivo docker-compose.yml

Abre el archivo docker-compose.yml con un editor de texto como nano para configurarlo. Usa el siguiente comando:

>nano docker-compose.yml

Dentro del archivo, copia y pega la siguiente configuración:



version: '2.2'

services:

mongo:
  
    image: mongo:4.0.4
    
    restart: always
    
    container_name: monguito
    
    environment:
      - MONGODB_USER="user"
      - MONGODB_PASS="pass"	
      
    volumes:
      - ./monguitodata:/data/db
      - ./monguitodata/log:/var/log/mongodb/
    ports:
      - "27017:27017"

      
  Notas Importantes:

    Cambia los valores de MONGO_INITDB_ROOT_USERNAME=user y MONGO_INITDB_ROOT_PASSWORD=pass según tus necesidades.
    
    Los volúmenes ./monguitodata:/data/db y ./monguitodata/log:/var/log/mongodb/ mapean carpetas locales a las carpetas dentro del contenedor.

Para guardar los cambios en nano, presiona Ctrl + O, luego Enter, y finalmente Ctrl + X para salir del editor.

__________________________________________________________________________________________________________________________________________________________________________________________
Paso 4: Hacer el Script Ejecutable

Para poder ejecutar el script, necesitas otorgar permisos de ejecución:

>chmod u+x mongo.sh

__________________________________________________________________________________________________________________________________________________________________________________________
Paso 5: Ejecutar el Script

Ejecuta el script que acabas de configurar:

>./mongo.sh

__________________________________________________________________________________________________________________________________________________________________________________________

Paso 6: Editar y Configurar el Script de Ejecución

Para completar la configuración, crea y edita un archivo de script adicional que automatice la creación y el inicio del contenedor.

6.1: Crear y Editar el Archivo mongo.sh

Usa cat para crear y editar el archivo mongo.sh:

>cat > mongo.sh

6.2: Pega el Siguiente Contenido en el Script

#!/bin/bash

# Crear carpeta para volumen de MongoDB:
>mkdir -p monguitodata/log

# Iniciar el contenedor:
>sudo docker-compose up -d

# Mostrar mensaje de inicio:
>echo "Monguito se está iniciando..."

# Entrar en el contenedor:
>sudo docker exec -it monguito bash

Presiona Ctrl + D para finalizar la edición y guardar el archivo.


___________________________________________________________________________________________________________________________________________________________________________________

Conclusión

Ahora, con el script mongo.sh configurado y ejecutado, tu contenedor de MongoDB debería estar en funcionamiento. Puedes usar este contenedor para tus necesidades de desarrollo y manipulación de bases de datos MongoDB.

Realizado por Jorge Sislema


