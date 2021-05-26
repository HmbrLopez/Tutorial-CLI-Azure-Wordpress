# Tutorial-CLI-Azure-Wordpress
Tutorial Wordpress Cli Linux

🐧
<h1>Como Instalar Wordpress En Ubuntu Server Azure</h1>

## Suplanta las palabras en mayúsculas con tu info
**Este es para obtener las listas de ubicaciones de servidores que tiene Azure**

    az account list-locations
  
**Con este creas un grupo de recursos dejar centralus**

    az group create --name NOMBRE_GRUPO_DE_RECURSOS --location centralus
    
**Para crear una maquina virtual en tu grupo de recursos**
        
      az vm create \
        --resource-group NOMBRE_GRUPO_DE_RECURSOS \
        --location centralus \
        --name NOMBRE_MAQUINA_VIRTUAL \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys     
  
  **Copia aquí tu IP**
  
        publicIpAddress": "23.99.204.43
        
        
**Con este comando obtienes todas las direcciones IP de todas las maquinas virtuales de tu grupo de recursos**

        az network public-ip list --resource-group NOMBRE_GRUPO_DE_RECURSOS --query [].ipAddress
        
**Con este comando abres el puerto 80 que es necesario para que se funcione la conexion de la pagina** 

        az vm open-port --port 80 --resource-group NOMBRE_GRUPO_DE_RECURSOS --name NOMBRE_MAQUINA_VIRTUAL

**Con este comando accedes a la máquina virtual**

        ssh azureuser@TU_DIRECCION_IP
        
**Un comando de Prueba si la maquina funciona**

        sudo apt-get moo        
        
**Con este comando actualizas la maquina**

        sudo apt-get update
        
 
 **Install Apache, PHP, and MySQL Para Poder Utilizar Wordpress**
 
LAMP (Linux, Apache, MariaDB y PHP) es un conjunto de aplicaciones ideales para el trabajo web y gestión de datos, en primer lugar, instalamos Apache si no lo tenemos con el siguiente comando:

    sudo apt install apache2
      
    
Todos los archivos de configuración de Apache2 están en el directorio /etc/apache2 y el archivo de configuración principal es /etc//etc/apache2/apache2.conf.

**Te da la versión de Apache y verifica si está bien instalado**

    apache2 -v  

Vemos el estado de Apache con el siguiente comando:

    sudo systemctl status apache2
    
Habilitamos Apache en el arranque de Ubuntu:

    sudo systemctl is-enabled apache2
    
Ahora instalaremos el gestor de base de datos el cual será MariaDB, para ello ejecutamos lo siguiente:

    sudo apt install mariadb-server mariadb-client
    
    
Comprobamos el estado de MariaDB:

    sudo systemctl status mariadb
    

Habilitamos su inicio desde el arranque:

    sudo systemctl is-enabled mariadb
    
El siguiente paso será asegurar la instalación de MariaDB con el siguiente comando:

    sudo mysql_secure_installation
    
Ingresamos la contraseña deseada para el usuario root y luego respondemos lo siguiente:
    
    Set a root password? [Y/n] y
    Remove anonymous users? [Y/n] y
    Disallow root login remotely? [Y/n] y
    Remove test database and access to it? [Y/n] y
    Reload privilege tables now? [Y/n] y  
    
**Te da la versión de MySQL y verifica si está bien instalado**

    mysql -V

Finalmente instalamos PHP y sus complementos con el siguiente comando:

    sudo apt install php libapache2-mod-php php-mysql
    
    
**Te da la versión de PHP y verifica si está bien instalado**

    php -v
    
 
**Crear base de datos para wordpress**

Lo primero conectar con el motor de BBDD, con un usuario con privilegios para crear otros usuario y bases de datos, suele ser el usuario root

    sudo mysql -u root -p
    
(pedirá la clave).

Una vez dentro a mi me gusta ver las bases de datos

    show databases;
    
Para crear el usuario:

    CREATE USER ‘hmbr’@‘localhost' IDENTIFIED VIA mysql_native_password;
    
🐧 Ahora le establecemos una password:

    SET PASSWORD FOR ‘hmbr’@‘localhost' = PASSWORD(‘12345’);
    
🐧 Creamos la base de datos:
      
    CREATE DATABASE IF NOT EXISTS `hmbr`;
    
🐧 Le damos todos los privilegios sobre esta base de datos al usuario recién creado:
    
    GRANT ALL PRIVILEGES ON `hmbr`.* TO ‘hmbr’@‘localhost';

