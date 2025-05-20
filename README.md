# Tarea Xampp en Linux Ubuntu Server - alu16v
Configurar un servidor de Ubuntu Server 24.04 LTS para alojar una web simple utilizando XAMPP  

## 1. Instalación del servidor *(apartados 1 y 2)*
Una vez creada la máquina virtual de Ubuntu Server en VirtualBox, solo hace falta añadirle desde la configuración un Adaptador Puente y comprobar su dirección IP (una opción cómoda es mediante el comando iconfig de *net-tools*.
En la siguiente imagen se puede comprobar la conexión entre ambas máquinas virtuales con el comando ping.
![image](https://github.com/user-attachments/assets/d2102d7e-ea26-4f86-9244-6a6287b7430e)


## 2. Instalación XAMPP *(apartado 3)*
Mediante el comando ```wget``` se puede descargar el instalador de xampp directamente en el servidor mediante su cli. En mi caso escogí la versión 8.2.0 del sourceforge de excellmedia. 
Una vez descargado, se le da permisos de ejecución con ```chmod 755 [nombre del archivo]```, y se instala con ```sudo ./[nombre del archivo]```. Se instalará en /otp/lampp, y se inicia el servicio con ````sudo /otp/lampp/lampp start```. Esto iniciará los servicios Apache, MySQL y ProFTPD. Una vez iniciados, se puede acceder desde cualquier ordenador en la misma red yendo a la dirección IP del servidor en un navegador.
![image](https://github.com/user-attachments/assets/56545369-5311-477a-9483-6e648eb9af9e)

## 3. Creación de usuarios *(apartados 4, 5 y 6)*
Para añadir usuarios, siendo usuario root o con permisos de administrador, se hace con el comando ```sudo adduser [nombre de usuario]```, y a continuación pedirá que se teclee la contraseña y se vuelva a teclear para confirmar. Después pide otros datos, como nombre completo, número de puerta... pero no es necesario.
En mi caso instalé el protocolo SSH con la instalación de Ubuntu Server, ya que me dio esa opción. Si no, se instala con ```sudo apt-get install ssh```, y se inicia con ```sudo systemctl enable ssh```>```sudo systemctl start ssh```. Después, en un terminal en el ordenador cliente, el comando para iniciar sesión en la cli del servidor es ```ssh 'usuario'@'dirección del servidor'```, y autenticarse con la contraseña del usuario.

En la siguiente imagen se puede comprobar cómo inicio sesión desde un Ubuntu Desktop en el servidor haciendo SSH, tanto con el usuario *cliente1* como *cliente2*.

![image](https://github.com/user-attachments/assets/a5017a9c-6b98-40d1-891d-b5302e9c2c8b)

## 4. Crear y publicar una página web *(apartado 7)*
Xampp coge las páginas web de la carpeta /opt/lampp/htdocs/index.html, asi que se puede crear una página para comprobar que funciona en esa ubicación y aparecerá inmediatamente. Creé una estructura básica de HTML5 con el comando ```sudo nano /opt/lampp/htdocs/index.html```, pero también se podría copiar con comandos un sitio web entero haciendo uso de la conexión ssh previamente iniciada.
Después, para garantizar que el servicio lo pueda leer, se usa el comando ```sudo chown nobody:nogroup /opt/lampp/htdocs/index.html```, que cambia el propietario del archivo. 
Se podría reiniciar el servicio para asegurarse de que se han guardado los cambios en la página web, pero en mi caso no fue necesario.

En la siguiente imagen se puede comprobar cómo se accede al sitio web en [ip del servidor]/index.html.
![image](https://github.com/user-attachments/assets/72db23eb-e996-4e8b-b24d-9657e83d8020)
