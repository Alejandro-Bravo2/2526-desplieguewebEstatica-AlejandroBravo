# Práctica: Despliegue de Web Estática con Docker
**Alejandro Bravo Calderón - 2º DAW**

## Descripción del proyecto

Esta práctica consiste en montar un servidor web Nginx con Docker Compose para servir dos páginas web estáticas. Además, he configurado un servidor SFTP para poder subir los archivos mediante FileZilla, simulando un entorno de despliegue real.

## Estructura del proyecto

El proyecto tiene dos servicios en Docker:
- **Nginx**: Servidor web que sirve las páginas en el puerto 8080
- **SFTP**: Servidor para transferir archivos por FileZilla en el puerto 2222

Los dos contenedores comparten una carpeta (`tarea_despliegueWebEstatica`) para que cuando suba archivos por SFTP, aparezcan automáticamente en la web.

## Docker compose


## Proceso de despliegue

### 1. Transferencia de archivos con FileZilla

Primero me conecté al servidor SFTP usando FileZilla para subir los archivos de las webs:

**Transferencia del primer archivo:**
![alt text](image-4.png)

**Transferencia del archivo index.html:**
![alt text](image-5.png)

**Archivos en local después de la transferencia con FileZilla:**
![alt text](image-6.png)

### 2. Verificación de las webs

Una vez subidos los archivos, comprobé que todo funcionaba correctamente desde el navegador.

**Página principal (CloudAcademy) en http://localhost:8080:**
![alt text](image-7.png)

**Página del reloj en http://localhost:8080/reloj/:**
![alt text](image-8.png)

## Conclusión

La práctica ha funcionado bien. Las dos webs se ven correctamente y el sistema de transferencia por SFTP funciona como debería. Cuando subo un archivo por FileZilla, aparece inmediatamente en el navegador sin tener que reiniciar nada.

## Volúmenes: Fijaos bien en las rutas internas de los contenedores. Nginx suele servir archivos desde /usr/share/nginx/html. Tendréis que averiguar en qué ruta guarda los archivos el contenedor SFTP que elijáis y "conectar" ambas rutas usando el mismo volumen.




Usuarios: Si usáis la imagen atmoz/sftp, leed su documentación sobre cómo pasar el usuario y la contraseña en la configuración del command o variables de entorno.
Permisos con SFTP: Si intentan subir archivos con Filezilla directamente a /var/www/nombre_web/html (como sugieres en el texto: "buscamos la carpeta donde queremos subirla... la subimos al servidor"), les dará un error de "Permiso denegado", porque su usuario no tiene permisos de escritura en una carpeta propiedad de www-data. Para la solución: Subir los archivos a una carpeta temporal y luego los muevan con sudo mv desde la la terminal, o añadir un paso donde añaden su usuario al grupo www-data y dan permisos de escritura al grupo (chmod g+w).