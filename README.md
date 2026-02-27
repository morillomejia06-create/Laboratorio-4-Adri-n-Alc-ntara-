# Laboratorio-4-Adri-n-Alc-ntara-
Comandos utilizados en las practicas de Linux

===================================
PRACTICA 4 – SERVIDOR HTTP (APACHE)
===================================

**----- INSTALACION -----**

# Actualizar repositorios
sudo apt update
sudo apt upgrade -y

# Instalar Apache
sudo apt install apache2 -y

# Verificar estado del servicio
sudo systemctl status apache2

# Habilitar al iniciar el sistema
sudo systemctl enable apache2

# Reiniciar servicio
sudo systemctl restart apache2

**----- PRUEBA DESDE NAVEGADOR -----**

En el navegador (desde Windows)
http://IP_DEL_SERVIDOR

Debe mostrarse la pagina por defecto de Apache

**----- CREAR PAGINA PERSONALIZADA -----**
# Crear carpeta 
sudo mkdir /var/www/hola

# Editar archivo principal
sudo nano /var/www/html/index.html

Ejemplo de contenido:
<h1>Servidor Web Funcionando Correctamente</h1>

# Guardar cambios
ctrl+o enter ctrl+x 

**----- HOST VIRTUAL ----**

# Crear archivo de configuracion 
sudo nano /etc/apache2/sites-available/hola.conf

# Activar sitio 
sudo a2ensite hola.conf

# Reiniciar Apache
sudo systemctl restart apache2

# Probar en el navegador
http://IP:80

Se realiza lo mismo con el otro website de los datos personales.

===================================
PRACTICA 5 – SERVIDOR DE CORREOS
===================================

**----- INSTALACION POSTFIX -----**

# Instalar servicio de correo
sudo apt install postfix -y

Seleccionar:
Internet Site
Nombre del sistema: dominio.local (ejemplo)

**----- VERIFICAR SERVICIO -----**

sudo systemctl status postfix

# Habilitar al iniciar
sudo systemctl enable postfix

# Reiniciar servicio
sudo systemctl restart postfix

# Instalar herramienta para enviar correos
sudo apt install mailutils -y

**----- PRUEBA DE ENVIO LOCAL -----**

Enviar correo de prueba
echo "Correo de prueba" | mail -s "Prueba" usuario

# Verificar si se envió
sudo tail -f /var/log/mail.log

Si ves: status=sent. Esta enviado. 


===================================
PRACTICA 6 – IMPRESORA VIRTUAL PDF (CUPS)
===================================

# Instalar CUPS
sudo apt install cups -y

# Iniciar servicio
sudo systemctl start cups

# Habilitar al iniciar
sudo systemctl enable cups

# Verificar estado
sudo systemctl status cups

# Reiniciar CUPS:
sudo systemctl restart cups


**----- INSTALAR IMPRESORA PDF -----**

sudo apt install printer-driver-cups-pdf -y

# Verificar instalación
dpkg -l | grep cups-pdf


**----- ACCEDER A CUPS DESDE NAVEGADOR -----**

http://IP_DEL_SERVIDOR:631

Ir a:
Administration → Add Printer
Seleccionar CUPS-PDF
Nombre: PDF
Add Printer

**----- PRUEBA DESDE SERVIDOR -----**

Crear archivo de prueba
echo "Prueba de impresion" > prueba.txt

Enviar a imprimir
lp -d PDF prueba.txt

Verificar PDF generado
ls ~/PDF

**----- CONFIGURACION EN WINDOWS -----**

Agregar impresora de red desde el panel de control

Puerto:
http://IP_DEL_SERVIDOR:631/printers/PDF


**----- PRUEBA DESDE WORD -----**

Abrir documento en Word
Seleccionar impresora del servidor
Clic en Imprimir

Verificar en el servidor
ls ~/PDF

Debe generarse archivo PDF automáticamente
