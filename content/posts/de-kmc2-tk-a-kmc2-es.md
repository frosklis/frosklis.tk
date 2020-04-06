---
title: "De kmc2.tk a kmc2.es"
date: 2020-04-06T14:41:09+02:00
draft: true
---

[Mi otro blog, al igual que este, tiene un dominio tk](https://kmc2.tk). También está escrito en español, [así que he cambiado el dominio a .es](https://kmc2.es). Aprovecho para contar cómo están montados mis dos blogs.

Empecé en esto del blogging usando [wordpress], una plataforma estupenda presente en más del 20% de la web. Wordpress está muy bien, pagando un poco es muy fácil de usar y no tiene. Después, por aprender, lo migré a [Google Appengine](https://cloud.google.com/appengine). Luego a [Jekyll]. Y, espero que sea ya la última vez, a [Hugo].

El motivo de abandonar [wordpress] es que quería más control. App engine de google fue un ejercicio muy bueno, porque aprendí mucho sobre APIs y sobre Google. De eso hace tiempo ya, pero me encantó usar el [data store](https://cloud.google.com/datastore) y en general la suite d Google Cloud, que para el uso que yo le daba era prácticamente gratuita, máxime cuando las fotos las tenía almacenadas en [flickr](https://www.flickr.com/photos/136165817@N06/).

Un inciso, las fotos siempre han sido un problema: hay que tenerlas en muchos tamaños, si cambias el diseño de la web hay que regenerarlas. Hice bastantes scripts para hacer cosas de ese estilo. Es un poco más complicado además cuando la foto original está en RAW. Y no quiero pagar varias veces por almacenar las mismas fotos, ahora mismo las tengo en [lightroom](https://lightroom.adobe.com), que no es nada barato pero me da acceso al software que ya tenía.

Con lo de las fotos y con el problema que suponía mantener una plataforma par blogs propia, busqué una alternativa que me permitiera jugar con la tecnología sólo si yo quería y descubrí [Jekyll]. Jekyll es un generador de páginas estático. La ventaja de generar las páginas de forma estática es que para alojar el blog vale cualquier cosa y la falta de dinamismo se puede suplir con Javascript y con servicios de terceros, por ejemplo [Disqus](https://disqus.com/) para comentarios.

Pero [Jekyll] me resultaba muy difícil de personalizar porque Ruby no lo domino bien, así que otra vez busqué una alternativa y encontré [Hugo], que es lo que uso ahora.

En ese sentido, actualmente mis dos blogs tienen la misma configuración:

1. Están alojados en [github](https://github.com/) utilizando [github pages](https://pages.github.com).
2. La generación de los HTML no la hago yo si no que la tengo automatizada con [Travis](https://travis-ci.com/)
3. Utilizo [Cloudflare] como CDN. 

Si el código de la web es abierto, todo lo anterior es gratuito. Lo único por lo que hay que pagar es el dominio. Y por eso usaba un dominio .tk, porque eran gratis. Ya no lo son, o sí lo son pero sólo durante un tiempo. Y salvo el precio, para todo lo demás los dominios .tk son malos: la propia web de gestión es horrorosa y de cara a posicionamiento en buscadores e imagen en general, no es un dominio bueno. No me importaría, eso sí, conocer la isla de [Tokelau](https://en.wikipedia.org/wiki/Tokelau) que da nombre al dominio, parece que están administradas por Estados Unidos.

Uno de los motivos de usar [Cloudflare] es que realmente es muy malo el DNS. Pero además, y sobre todo cuando todo esto estaba alojado en AppEngine, tener un CDN quita tráfico del servidor y eso se traduce en menos dinero. Además la interfaz de Cloudflare es muy buena y se puede acceder por API, lo cual permite borrar el caché cada vez que se genera una versión nueva de la web.

# Cambiar el dominio

Dicho todo eso, ¿qué hay que hacer para cambiar el dominio?

Lo primero es esperar porque los cambios de dominio tienen que propagarse por los DNS del mundo. No es inmediato, tarda unas horas. [DNSchecker es una web que se puede usar para comprobarlo](https://dnschecker.org/).

Con el dominio comprado, para seguir teniéndolo en Cloudflare hay que añadirlo a través de su interfaz gráfica y cambiar en el proveedor los DNS para que apunten a estos dos:
- gabe.ns.cloudflare.com
- dawn.ns.cloudflare.com

Cloudflare importa la configuración del dominio automáticamente. Además yo marco cosas como que se ofrezcan versiones minificadas del HTML, CSS y Javascript, proporciono un certificado autofirmado (en Cloudflare es encriptación "fulll") y digo que siempre se use HTTPS.

Independientemente de que se use o no Cloudflare, hay que decir en el DNS que queremos que apunte a la ip donde esté el servidor correspondiente, [aquí se ven los de Github](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain).

Después en github, desde el propio repositorio la ayuda dice que hay que cambiar el dominio de forma manual. En realidad no es necesario, sólo hay que cambiar el fichero CNAME en la rama gh-pages (o la rama desde la que se está cambiando el repositorio). Y como lo tengo todo automatizado, ya está.

Próximamente cambiaré el dominio de este blog también.

[wordpress]: https://www.wordpress.org
[Jekyll]: https://jekyllrb.com/
[Hugo]: https://gohugo.io/
[Cloudflare]: (https://www.cloudflare.com/)
