---
title: "Cómo organizo mis fotos"
date: 2021-05-12T12:32:43+02:00
draft: true
---

A lo largo de los años mi mujer y yo hemos hecho bastantes fotos, sobre todo teniendo en cuenta que no nos dedicamos a ello. Hemos hecho unas 50.000 y subiendo. Hacemos fotos con nuestros móviles y también con nuestras cámaras. Nos gusta retocarlas de vez en cuando (disparamos en raw) y compartirlas con el resto de la familia y amigos.

Anteriormente usábamos Lightroom, la versión por suscripción, pero tiene el problema de una sensación de pérdida de control y el precio, que se suma al que ya pagamos por el plan familiar de Dropbox.

# Cómo funciona en la práctica

Uno de los objetivos que tenía al organizar mis fotos era que fuera bastante automatizado y fácil de usar. Principalmente hacemos fotos, las retocamos de vez en cuando, las compartimos con gente y las clasificamos un poco.

## Hace fotos

Podemos hacer fotos con cualquier cámara. 
Si las hacemos con el móvil, tenemos configurada la aplicación de Dropbox para que haga copia de seguridad de las fotos que hacemos.
Si las hacemos con una cámara, las importamos directamente a una carpeta concreta que llamamos ```en_proceso```. 

Las de Dropbox aparecen mágicamente en esa carpeta ```en_proceso``` también. Además aparecen con el nombre cambiado de mode que las fotos tienen por nombre la fecha y la hora en la que se tomaron, por ejemplo ```20111601-131512.jpg```. Eso sería una foto tomada el 1 de junio de 2011 a la una y cuarto. Muy cómodo para organizarlas luego.

## Edita fotos y selecciona

Nosotros usamos [darktable](https://www.darktable.org/) y [digikam](https://www.digikam.org/). En teoría podría valer con cualquier programa, pero Darktable tiene la ventaja de que me permite automatizar la creación de imágenes jpg.

Lo que hacemos aquí es ver nuestras fotos, borrar las que no nos gustan y hacer los retoques adecuados. Si queremos, podemos ponerles etiquetas, aunque no es necesario, se puede hacer en cualquier punto del proceso. Digikam ayuda a lo de poner etiquetas porque tiene cosas como reconocimiento facial y un organizador de etiquetas muy superior al de Darktable.

Como las fotos están en Dropbox, esta carpeta ```en_proceso``` también lo está y se puede hacer en cualquier ordenador, ya sea cada uno de nuestros portátiles o en un ordenador fijo que tenemos en casa (un Intel NUC).

Cuando termina, mueve las fotos a la carpeta ```terminadas```, y ya está.

## Crea colecciones (opcional)

Esta parte no es la más amigable del proceso, aunque técnicamente estoy contento con la solución adoptada. Hay un fichero de configuración que se llama ```colecciones.yml``` donde se define cada colección con unos filtros en sintaxis SQL. Suena peor de lo que es en realidad. Un ejemplo:
```
- name: 5 estrellas
  folder: cinco estrellas
  rule: rating = 5
```

Se define cómo se llama la colección, en qué carpeta dejarla y una regla para decidir qué fotos van dentro.

## Las comparte, las ve

Las fotos se ven en jpg, no en raw. Para ello, todas las fotos aparecen mágicamente en una carpeta que se llama ```jpeg``` y dentro de esa carpeta están ordenadas en carpetas por fecha y día.

También tenemos la carpeta de colecciones, donde están organizadas según las colecciones que queramos. Nuestras mejores fotos, nuestros viajes, las fotos de una persona en concreto, etc. Estas son las carpetas que solemos compartir con gente utilizando la funcionalidad de Dropbox. También son las que sincronizamos en local con nuestros ordenadores o en algún sitio para utilizarlas como fondo de pantalla.

Este último punto, el de usarlas como fondo de pantalla, lo utlizamos en la tele. Tengo una Raspberry Pi con Kodi y automáticamente aparecen como salvapantallas las fotos de la colección "5 estrellas".

## Las vuelve a editar, retocar, seleccionar

Del mismo modo que se hacía en la carpeta ```en_proceso``` las fotos originales las tenemos guardadas en la carpeta ```negativos``` organizadas por año y día, de modo que son fáciles de encontrar. Con Darktable las podemos seguir retocando, o borrarlas. Podemos añadir etiquetas a las fotos para que sea más fácil incluirlas en una colección.

Y cuando se hace esto no hay que hacer nada más. Las fotos actualizadas aparecen mágicamente en todas partes, la carpeta de colecciones, la carpeta de jpgs, en los ordenadores, dispositivos móviles, etc.

# Cómo está hecho

Las piezas centrales de esto son:
- Dropbox, que utilizamos para sincronizar entre dispositivos de forma automática.
- Un ordenador (Intel NUC) suficientemente potente y con capacidad de disco duro suficiente como para tener las fotos en local. Con el *smart sync* de Dropbox funcionaría igual pero mucho más lentamente.
- Darktable para generar las imágenes finales a partir de los negativos.
- [Exiftool](https://exiftool.org/) para renombrar las imágenes y extraer metadatos.
- Un conjunto de scripts que se ejecutan automáticamente en el Intel NUC.

Todo el código lo tengo en un (repositorio git)[https://github.com/frosklis/picture_scripts] por si es útil para alguien. Evolucionará en el tiempo según mis necesidades.

## El Intel NUC

Tiene instalado Arch linux con KDE y los programas Digikam y Darktable. También tiene la BIOS tocada para convertirlo en un ordenador muy silencioso, a costa de renunciar a cierta potencia. Para ello el TurboBoost está deshabilitado y el ventilador configurado para que pueda funcionar a bajas revoluciones; en la configuración habitual, si no está apagado, trabaja como mínimo al 30%, lo cual es demasiado ruidoso.

Que sea silencioso es muy importante porque el ordenador está en casa y potencialmente se podría cambiar de sitio y poner en el salón detrás de la tele (tiene montaje VESA, quedaría totalmente oculto y decorativamente bien).

## Adquisición de fotos 

Todas las fotos tienen que llegar a la carpeta ```en_proceso```, que es una carpeta compartida en dropbox dentro del espacio familiar. 

Si las fotos vienen de una tarjeta SD, no hay que hacer nada especial. Simplemente al importarlas, hay que importarlas a esa carpeta.

En cambio las fotos del móvil tienen que aparecer mágicamente ahí. ¿Cómo?

Lo primero, en el Intel NUC hay configurados tres usuarios: el mío, el de mi mujer y uno especial que llamo "fotos". El mío y el de mi mujer tienen instalado dropbox y sincronizada la carpeta *camera uploads*, con lo cual todas las fotos que hacemos con el móvil aparecen ahí automáticamente. Importante: tenemos sincronizada solo esa carpeta, no todo Dropbox.

El usuario fotos tiene sincronizada, con Dropbox, la carpeta Fotos, dentro de la cual hay las siguientes carpetas:
- ```en_proceso```, que son fotos en las que estamos trabajando.
- ```terminado```, a donde van las fotos que hemos terminado de editar. Sólo están ahí temporalmente.
- ```negativos```, que son las fotos en formato raw o como vengan de la cámara. También se guardan los ficheros XMP que generan los programas de edición.
- ```jpeg```, que son las imágenes generadas en formato jpg y organizadas por año y fecha.
- ```colecciones```, donde aparecen las colecciones según se definen en un fichero de configuración. Si Dropbox entendiera bien los enlaces simbólicos, esto serían enlaces simbólicos en vez de ficheros jpg. Lo único que tendría que hacer es cambiar en un script la línea ```shutil.copy(symlink, destination)``` por ```os.symlink(symlink, destination)```

Volviendo a la adquisición de fotos en sí, para que las fotos de camera uploads aparezcan en ```en_proceso``` hay un servicio del sistema configurado para hacer lo siguiente:
- Arrancar dropbox en modo demonio para los tres usuarios antes de que hagan login
- Mover los archivos de la carpeta de camera uploads a ```en_proceso``` cada vez que haya algún cmabio en la de ```camera uploads``` del usuario. Esto se hace con ```inotify```. Otra opción habría sido ejecutar esto por ejemplo cada hora, pero con inotify se consigue una inmediatez muy cómoda.

## Edición de fotos

Técnicamente esto es poco flexible. Sólo funciona bien con Darktable. Aunque podría hacerse con cualquier otro programa, la automatización posterior no funcionaría o, lo que es peor, tendría apariencia de funcionar pero no daría los resultados adecuados.

El motivo de esto es la falta de estandarización en la industria fotográfica. 
Cuando se trabaja con ficheros RAW, se tienen dos ficheros el original de la cámara (en mi caso es un fichero ```.nef``` porque tengo una Nikon, podría ser ```cr2``` con una Canon) y un fichero ```xmp``` (*sidecar file* en inglés) que genera el programa de edición. Las etiquetas de las fotos forman parte de xmp y son universales (más o menos) pero los ajustes de edició no: en general, una foto editada por el programa A no puede ser procesada por el programa B, no hay interoperabilidad en ese sentido.

Y por eso usamos Darktable. Darktable se parece a Lightroom, sólo que tiene muchas más opciones y peor (bastante peor) interfaz; aunque se parece estéticamente, no es tan cómodo de usar como Lightroom. Dicho eso, si Lightroom es un 10, Darktable es un 8 por lo menos.

Digikam, en cambio, al procesar una foto no genera un XMP (lo puede generar, pero es un "además de", no un "en vez de") sino que genera directamente un jpg en la misma carpeta que la foto. Esto no encaja con el flujo de trabajo que yo quiero.

Darktable tiene una cosa genial para los automatismos: ```darktable-cli```. Con esta utilidad de línea de comandos se pueden generar los jpg por línea de comandos. Esto ayuda a los siguientes pasos del automatismo.

## Terminar de editar las fotos

Este es un paso manual apoyado por un automatismo. Es el usuario el que manualmente tiene que mover las fotos de ```en_proceso``` a ```terminado```. Cuando esto ocurre pasan dos cosas:
- Se mueven los ficheros (xmp incluido) a ```negativos``` organizándolos por año y fecha.
- Se dispara la réplica de ```negativos``` a ```jpeg```, es decir: se genera la imagen jpg y se guarda en la carpeta de jpegs. Esta carpeta replica la estructura de la carpeta de negativos.

Además, si de una foto se han hecho varias versiones, se generan todos los jpgs.

## Sincronismo

Dada la flexibilidad que quiero dar al sistema, el sincronismo es algo complejo. La flexibilidad consiste en que si yo hago una modificación de las etiquetas en cualquiera de las carpetas (negativos, jpeg o colecciones), se debe actualizar en todos los demás sitios. Si funcionaran bien los enlaces simbólicos en dropbox, sincronizar con colecciones no sería un problema.

Además, dado el alto volumen de fotos, esto no es algo que se pueda a hacer para todas fotos siempre porque leer los metadatos EXIF de más de cincuenta mil fotos es fácil pero lento, demasiado lento para que sea usable.

Los scripts se pueden lanzar manualmente, cada cierto tiempo o respondiendo a eventos (inotify) y principalmente hacen lo siguiente:
- se mantiene un fichero que llamo *exif_info.tsv* que es una tabla de características de la foto: nombre, carpeta, fichero raw del que deriva, etiquetas, posición gps, calificación (estrellas), título y descripción. Se genera con ```exiftool```:

```
exiftool "$1" -r -T -n -api MissingTagValue^= -Rating -GPSlatitude -GPSlongitude -datetimeoriginal -directory -filename -title -description -derivedfrom -filemodifydate -subject -hierarchicalsubject -Make -Model -ImageWidth -ImageHeight -Aperture -ExposureTime -ISO > "$1"/picture_data.tsv
```

- Se busca en las carpetas correspondientes. ¿Qué? Ficheros modificados después de la fecha de generación de esa tabla.
- En la comprobación periódica se actualiza también la tabla para eliminar de la tabla ficheros que hayan sido eliminados.
- Se hace la correspondencia entre carpetas.
- Se actualizan las etiquetas, si hay cambios.
- Se regeneran las imágenes, si procede.

Toda esta complejidad, repito, es para no hacerlo de cero cada vez. Por ejemplo, la primera vez que generé masivamente los jpg de todas las imágenes, llevó unos dos días. Es cierto que hay optimizaciones que se podrían hacer pero el caso es que llleva demasiado tiempo. Que lleve demasiado tiempo impide en la práctica hacer algo tan sencillo como pedir que el script se ejecute cada hora porque el tiempo de ejecución es más de una hora.

Esta complejidad reduce el tiempo a segundos.

## Generación de colecciones 

Las colecciones son fáciles de generar. Tengo un fichero yaml que las configura, donde el parámetro más importante es ```rule```, que es un filtro sql que puede incorporar todas las columnas generadas con exiftool. Esto lo hago en python con el paquete ```pandasql``` que permite usar sintaxis SQL para los DataFrames de pandas.

Volviendo al ejemplo que ponía arriba, esta es una definición real de colección.
```
- name: 5 estrellas
  folder: cinco estrellas
  rule: rating = 5
```

El programa en python que tengo ejecuta la consulta ```select directory, filename from fotos where rating = 5```. Directamente lo que se mete en *rule* es lo que va al filtro de la consulta. Después borra el directorio *cinco estrellas* y lo vuelve a generar copiando en él las fotos correspondientes.

Sería mejor un enlace simbólico, pero el enlace simbólico sólo funciona si tienes sincronizada también la carpeta a la que hace referencia, algo que normalmente no quiero porque estas son las carpetas que más se utilizan para realmente usar las fotos después:
- Compartirlas con gente: comparto la colección con gente dándoles acceso a a la carpeta en Dropbox.
- Usarlas como salvapantallas en la tele.

## Salvapantallas en la tele

No he encontrado la forma de que el salvapantallas del Chromecast lea las fotos de un lugar distingo a Google Photos. Además, Google Photos va a dejar de ser gratis y no quiero empezar a pagar por otra nube. Mi opinión sobre Google Drive es que, comparado con Dropbox, es muy malo ya que el smart sync no funciona. Tienes que tener o cuenta de empresa (no vale usuario normal que paga) o hacer cosas raras con FUSE que no serían nada amigables para el usuario.

Lo que sí tengo configurado es Kodi. Tengo Kodi instalado en una Raspberry Pi con un disco duro que utilizo de media center y tengo puesta debajo de la tele. Decorativamente ocupa muy poco y no hace ruido.

No hay un cliente oficial de dropbox para Raspberry Pi, porque Dropbox no da soporte a arquitecturas de procesador ARM (tengo dudas de cómo funciona en los Mac nuevos, que seguro que lo hacen funcionar pero eso no se trasladará al mundo linux). Lo que utilizo entonces es [´´´rclone´´´](https://rclone.org/) y un comando en cron que se repite cada tres horas que lo que hace es sincronizar la carpeta de colecciones:

```rclone sync dropbox:Espacio\ Familiar/Fotos/colecciones /media/kmc2/fotos/```

# Resumen

Con todos los automatismos que hay por detrás consigo:

- Que solo me tenga que preocupar de hacer fotos y de editarlas.
- Ver las fotos en la tele como salvapantallas.
- Tenerlas disponibles en el móvil.
- Poder compartirlas con quien yo quiera.
