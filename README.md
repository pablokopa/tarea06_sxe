# TAREA06_SXE
---
### Creación y configuración del archivo.

<details>
<summary> <b> 1. Para crear y abrir un archivo de configuración: </b></summary>
<br>

```bash
# Crea el archivo
touch docker-compose.yaml

# Abre el archivo para editarlo
nano docker-compose.yaml
```
</details>

<details>
<summary> <b> 2. Configuración del archivo: </b></summary>
<br>

```yaml
services:
  mysql:
    image: mysql:latest
    container_name: base_mysql
    restart: always # Se reinicia siempre que el contenedor se detenga
    environment:
      MYSQL_DATABASE: prestashop_db # Especifica el nombre de la base de datos
      MYSQL_ROOT_PASSWORD: admin # Especifica la contraseña para el superusuario de la cuenta MySQL
    networks:
      - prestashop_network # Red que se va a crear y va a poder ser usada
  prestashop:
    image: prestashop/prestashop:latest
    container_name: prestashop
    restart: always
    depends_on:
      - mysql # Indica que prestashop depende primero del arranque de mysql 
    ports:
      - 8080:80 # Indica el puerto utilizado
    environment:
      DB_SERVER: base-mysql # Nombre de la base de datos mysql que se va a utilizar
      DB_NAME: prestashop_db # Sobreescribe el nombre de la base de datos
      DB_USER: root # Sobreescribe el nombre del usuario mysql por defecto
      DB_PASSWD: admin # Sobreescribe la contraseña mysql por defecto
    networks:
      - prestashop_network
networks:
    prestashop_network:
```
Una vez terminado el documento de configuración, lo lanzamos utilizando:
```bash
sudo docker compose up -d
```
![imagen](https://github.com/user-attachments/assets/8f2eb580-57c9-4b74-ae53-4046b48d34af)

</details>

<details>
<summary> <b> 3. Pruebas y configuración de PrestaShop: </b></summary>
<br>

```bash
# Utilizo en el navegador la ip de mi ordenador con el puerto seleccionado
10.0.9.153:8080
```
Una vez comprobado que todo funciona correctamente, me pongo a configurar todo desde el navegador:

**1. Asistente de instalación:**
  ![imagen](https://github.com/user-attachments/assets/6478ecce-f01d-4f02-99e1-f67ffc675c15)
  Indico el idioma y continuo...
  
**2. Se aceptan los terminos y condiciones:**
  ![imagen](https://github.com/user-attachments/assets/da8d4f4a-619d-484c-957e-23b0cadca3f7)

**3. Configuración de los datos de la tienda:**
  ![imagen](https://github.com/user-attachments/assets/350e1a67-324e-4e9f-b287-bf61a5174097)

**4. Configuración del contenido de la tienda:**
  ![imagen](https://github.com/user-attachments/assets/eacfeee2-1ade-479b-aa2c-77417cdcab61)

**5. Configuración de la base de datos:**
  ![imagen](https://github.com/user-attachments/assets/30ccbcef-f46f-4af7-975c-f31dc1a9a4ce)

**6. Comienza a cargar la tienda entera:**
  ![imagen](https://github.com/user-attachments/assets/6235109c-acf1-46e4-bcd1-00f949f56085)

**7. Finalizada la instalación:**
  ![imagen](https://github.com/user-attachments/assets/2ae5c256-aa9c-45e9-8024-16c17a57ad1b)
</details>

<details>
<summary> <b> 4. Para que la tienda funcione correctamente: </b></summary>
<br>
Es necesario eliminar la carpeta "install" por razones de seguridad:
  
```bash
# Eliminar carpeta install
sudo docker exec -it prestashop rm -rf /var/www/html/install
```

A continuación se entra en el siguiente enlace y nos pedirá iniciar sesión con los datos introducidos anteriormente:

```bash
10.0.9.153:8080/admin
```

Una vez iniciada sesión, ya podremos usar y personalizar la tienda como queramos.
</details>


