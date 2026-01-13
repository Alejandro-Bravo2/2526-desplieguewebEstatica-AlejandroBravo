1. NGINX EJECUTAR
docker run --name nginx-tarea -p 8080:80 -d nginx


docker exec -u root nginx-tarea mkdir -p /var/www/pruebas/html


git clone https://github.com/cloudacademy/static-website-example

docker cp static-website-example nginx-tarea:/var/www/pruebas/html


chown -R www-data:www-data /var/www/pruebas/html/


chmod -R 755 /var/www/pruebas/


Accedemos al puerto 8080 para comprobar si está funcionando:
![alt text](image.png)



