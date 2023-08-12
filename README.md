# ddwrt-hotspot-radius
Servidor Radius (daloradius) = perfiles, fichas,vouchers,tiempos, daloradius es instalado en el servidor web.
Ddwrt = Sistema para el router ,en este caso utilizamos archer c9, y alli configuramos el hotspot
Hotspotlogin = En la carpeta hotspot se encuentran los archivos del portal o inicio de logeo del cliente, estos van en la carpeta del servidor en /var/www/html/hotspot
## Daloradius
Utilizamos la instalacion descrita en el repositorio `https://github.com/abdiasriver/dalodeb`

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
