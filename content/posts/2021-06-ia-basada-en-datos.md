---
title: "Inteligencia artificial basada en datos"
date: 2021-06-14T14:00:25+02:00
draft: false
tags: [machine learning, Andrew Ng, Luis Von Ahn]
---

Desde hace ya unos años se viene hablando en mi trabajo de la necesidad de sistematizar la manera de hacer las cosas para ser más productivo en el ámbito de la inteligencia artificial (entendida en sentido amplio), es decir: cómo tener un modelo analítico en producción que sea un buen modelo.

[Este vídeo de Andrew Ng](https://youtu.be/06-AZXmwHjo) me ha hecho reflexionar y acordarme de otras cosas. En el vídeo sólo trata una idea, que luego desarrolla con ejemplos: los datos son más importantes que los algoritmos.

```
IA = datos + código
```

Su punto es que una vez se tienen los datos, lo que se suele hacer es tratar de mejorar el código. Sin embargo, si el 80% del trabajo es preparar datos, ¿por qué no se dedica más tiempo a asegurar su calidad? 

El problema principal del que habla es la consistencia entre etiquetas, que suele venir derivado de utilizar etiquetadores (personas que etiquetan) distintos. Eso introduce ruido en los modelos y, lógicamente, es más fácil arreglar un modelo etiquetando bien que mejorando la técnica de modelización.

Aquí me acordé de [Luis Von Ahn](https://es.wikipedia.org/wiki/Luis_von_Ahn) y una charla TED que dio explicando un proyecto suyo que [luego fue comprado y matado por Google](https://techcrunch.com/2006/09/01/google-image-labeler/) cuando ya no fue necesario. Luis Von Ahn luego fundó DuoLingo. El juego convierte una tarea aburrida, tediosa y difícil de hacer bien, etiquetar imágenes, en algo divertido de modo que durante años hubo gente (yo entre ellos) que de vez en cuando entraba ahí a hacerle trabajo gratis a Google. Se le pone una misma imagen a dos personas a la vez y las dos van escribiendo palabras asociadas a esa imagen, por ejemplo "perro". Cuando una palabra ha sido dicha por las dos personas, se pasa a la siguiente. Esa es la idea básica. [Este vídeo lo explica mejor que yo](https://www.ted.com/talks/luis_von_ahn_massive_scale_online_collaboration/transcript?language=es)

Luego lo mejoraron, añadieron opciones para dibujar cajas alrededor de objetos (marca dónde está el perro en esta imagen, el típico captcha de ahora), o introdujeron palabras tabú (no vale decir perro, hay que coincidir en otra cosa, la raza por ejemplo)... hasta que finalmente lo mataron. Google Image Labeler como tal ya no existe; esta y otras tareas tediosas de inteligencia artificial las tienen integradas en los [captchas](https://es.wikipedia.org/wiki/Captcha). Amazon también hace cosas de estas con mechanical turk. Y no todos los captcha que en la web son de Google.

Recuerdo cuando vi el vídeo de Luis Von Ahn original (no es el que puse antes, no lo encuentro) que me pareció una idea realmente brillante por su sencillez. Introducía lo que ahora se conoce como gamificación y resolvía este problema del que habla Andrew Ng de la sistematización en el etiquetado de categorías.

No es el único ejemplo del vídeo de Andrew Ng, también habla de otras cosas que se pueden hacer como *data augmentation*. Lo que me ha gustado del vídeo es que lo dice Andrew Ng y da validez a otras cosas que hago a veces.

Dos ejemplos. Mi mujer es médico y publica en revistas científicas en su especialidad. Cuando la veo trabajar en un artículo, siempre suele haber un modelo que trata de predecir algo y muy pocos casos (100, 200, de ese orden) para lo que un informático está acostumbrado. Hace un modelo y sale algo raro: siempre, lo primero que hace es revisar los datos de entrada y normalmente descubre errores en las etiquetas, que vienen de que los datos son recogidos por personas diferentes con criterios diferentes (y a veces, también, de meras equivocaciones).

El otro es más banal. Siempre que me viene alguien con un modelo que está mal pasamos por el mismo ciclo:

- ¿están bien los datos?
- sí
- ¿seguro?
- bueno...

Siempre he hecho revisar los datos, está bien que Andrew Ng ahora diga que es lo que hay que hacer.

Esto tiene implicaciones para las organizaciones. Las organizaciones con buenos datos pueden luego usarlos para tomar decisiones en las que confiar. Las que no tienen buenos datos se tienen que apañar de otra manera.

