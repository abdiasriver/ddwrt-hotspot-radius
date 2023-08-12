# ddwrt-hotspot-radius
Servidor Radius (daloradius) = perfiles, fichas,vouchers,tiempos, daloradius es instalado en el servidor web.

Ddwrt = Sistema para el router ,en este caso utilizamos archer c9, y alli configuramos el hotspot

Hotspotlogin = En la carpeta hotspot se encuentran los archivos del portal o inicio de logeo del cliente, estos van en la carpeta del servidor en /var/www/html/hotspot

El objetivo de este tutorial es tener un router en casa, el cual reparta internetpor medio de fichas o vouchers, en tiempo pausado y corrido, las cuales se administraran desde el servidor en la nube que contiene daloradius, el hotspotlogin.php o pagina de login en el cual el cliente introducira la ficha se encuentra alhojada en el servidor donde esta daloradius, y en el router ddwrt solo introduciremos su ubicacion o direccion url.
El router fisico tendra el sistema ddwrt , el cual se instala de acuerdo al tutorial de la pagina ddwrt.

## Daloradius
Utilizamos la instalacion descrita en el repositorio `https://github.com/abdiasriver/dalodeb`
tambien al finalizar la instalacion podemos importar la siguiente base de datos por si la que esta en el tutorial da algun error.

- Respaldo de la db
```
mysqldump -p -u root radius > dbackup.sql
```
- Restaurar db o importar base de datos.


```
git clone https://github.com/abdiasriver/ddwrt-hotspot-radius.git
mysql -p -u root radius < /root/ddwrt-hotspot-radius/chilichili.sql
```

## Hotspotlogin
Necesitamos una pagina php de logeo que se abrira como portal  hotspot cuando el usuario ingrese a nuestra wifi, esta pedira dos datos `usuario` y `password` y lo obtendra desde `daloradius` guardado en su base de datos.
Los archivos que utilizaremos estan en la carpeta `hotspot` viene modificado de acuerdo a mis necesidades.
- Usuario = mayusculas y numeros ,tambien se eliminan los espacios
- Password = mayusculas y numeros, tambien se eliminan los espacios.

_Igualmente se incluye la carpeta hotspotbk por si se desea usar la configuracion por defecto sin modificacion._

- Se descarga el repositorio
- Se mueven los archivos necesarios a la carpeta `/var/www/html` / servidor donde tenemos instalado daloradius o webserver.
- Se toma o copia la direccion del directorio donde queda localizado el archivo `hotspotlogin.php` en este tutorial queda en 
`http://ipdelservidor/hotspot/hotspotlogin.php` (esta sera usada en el router ddwrt)  ya que se encuentra en `/var/www/html/hotspot/hotspotlogin.php` 

## Ddwrt

- Primero obtnemos un router que soporte el sistema ddwrt, podremos saberlo ingresando al link `https://dd-wrt.com/support/router-database/` 
ingresando el nombre por ejemplo `archer` o `tp-link`
- Instalamos el sistema segun su tutorial y firmware.

1. En el router en `default` se coloca la configuracion parecida a esta.

![1setup](https://github.com/abdiasriver/ddwrt-hotspot-radius/assets/13319563/531cdc93-75d2-49d4-bed9-59719f4df5e4)

2. Despues para el hotspot se coloca lo siguiente de acuerdo a tus datos, de servidor radius y de la pagina php hotspotlogin.php.

![2hotspot](https://github.com/abdiasriver/ddwrt-hotspot-radius/assets/13319563/5b6fa918-e9e6-4390-ae60-47c3208dc158)

3. Alternativamente podemos subir el backup de configuracion, y al guardar y aplicar los cambios, los datos de acceso son.

   SSID = venta wifi prueba
   IP= 192.168.85.1
   USUARIO= Rivera
   CLAVE= 84River@B

   y cambiamos los datos en `services>hotspot`.

   4. Hacer pruebas creando usuarios en daloradius y logueando, igualmente perfiles de tiempos.
