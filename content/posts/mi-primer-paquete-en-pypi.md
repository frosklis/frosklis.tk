---
title: "Mi primer paquete en Pypi"
date: 2020-04-04T00:33:00+02:00
tags: [pypy, python, devops]
draft: false
---

He hecho [un paquete que he llamado cnml](https://github.com/frosklis/cn-machine-learning). Y lo estoy haciendo con fines autoformativos porque en los proyectos en los que trabajo nunca hago yo solo el trabajo de principio a fin. Mi conclusión es que cuando los proyectos es open source es mucho más fácil todo.

Todo empieza por tener un [código bien estructurado que se pueda instalar con setuptools](https://packaging.python.org/tutorials/packaging-projects/) y con crearse una cuenta en [pypi.org](https://pypi.org/). El único requisito es que el nombre del paquete no exista en pypi. Hecho eso, el paquete se puede subir por línea de comandos.

```bash
python setup.py dist
twine upload dist\*
```

Existen formas de automatizar lo anterior para que no sea necesario introducir el nombre de usuario y contraseña cada vez. Pero puestos a hacer eso, es mejor todavía hacer el ciclo completo de devops. Las prácticas de integración continua han mejorado mucho en los últimos años en cuanto a facilidad de uso. Ahora cualquiera lo puede hacer y contribuyen a que el código que tenemos sea mantenible. El desencadenante de todo es un commit. Se puede configurar github (o cualquier repositorio git) para que se desencaden acciones cada vez que ocurre algo. De hecho todos los grandes (github, gitlab, bitbucket y los internos de las plataformas en la nube de Amazon, Google y Microsoft) tienen APIs y se pueden conectar a terceros.

En el mundo open source el más famoso es [Jenkins](https://jenkins.io/). Los proveedores cloud tienen los suyos, Atlassian tiene el suyo. Lo que no me gusta de Jenkins es que tiene la barrera de entrada de que hace falta una infraestructura donde desplegarlo y hacerlo funcionar. Por eso yo he utilizado [Travis](https://travis-ci.com/) que funciona como servicio y es gratis para proyectos opensource. Podía haber utilizado también [Circle CI](https://circleci.com/).

Usando travis, lo único que hay que hacer es configurar el script .travis.yml que tiene que estar en la raíz del repositorio. [El mío es este](https://github.com/frosklis/cn-machine-learning/blob/master/.travis.yml) y hoy (4 de abril de 2020) tiene esta pinta:

```
language: python
script: pytest --cov=cnml
after_success: bash <(curl -s https://codecov.io/bash)
deploy:
  on:
    tags: true
  provider: pypi
  user: __token__
  password:
    secure: lUDdfS0w/P3YF7QospZmVHo0YWuFvuIwuteIQjzUuuJbOlA5K00iNHvuSp9cLx89pFL+dWO61ar2qYechdT1UdtKlvEZpbthgMACMkftY8F+LBUUs95DIph/1arUabr6ZOVyuc6kuc3YvaHMK78FjEB4J5YftRznp3LVLJPpWIjL1oOpPCbI4ETjxA+SvLqQGerKfTPUQWogjB/iDjLOczdWY9y6haHaF43svaFy7LWL2fxTC95PKhXANjGlME0mociZI1aIykZbOk58/WOLew4De7jCeN/sCathBKpq4cAV222RoAV73Rx9FWucS2U4XeRFGMUA8Bvv3T0gCoIzTN1C+wmN7g0SJBqVJkdSf/eN/fPo4sw8Fu0Ohs0iJr1f74h2z6EQeuKdMER5sxEUP1t1HWj8elQ1JwQT1h4AjXJSccGFJcYdvaP4SWr2+2x4uayPbg32R+5iQu0y7WMDtEH5KsNgJ9GBJ7YxLnLImx2UtkF6Iem/AYTYcP2PikW2RbOZM1A4DWakYvMAzegyWj8yjOp65tWfp2ntQ6LzjAJbauzBnVmGkoBAS2zQPv0kbiYoeE0pdQKaHqAl9tU0EjotN/n0DGKrEn0zay+GbMrL0uyDSwCkqHpxdBW5hCVJAzLQg3EJy8lVNyDp3EYq3Bl/bPqjRmWxJC6iLMXo4Z4=
```

Hace más cosas que simplemente generar el paquete:

1. genera el paquete
2. ejecuta los tests con cobertura
3. manda el informe de esa cobertura a codecov.io para verlo gráficamente
4. y sólo si el commit corresponde a una etiqueta sube el paquete a pypi

Lo que no tengo todavía bien resuelto es el nombrado de versiones. Utilizo el estándar [semver](https://semver.org), pero no de forma tan automatizada como me gustaría. En el repositorio en sí me gustaría hacer sólo lo que estoy haciendo ahora, que es tnner la versión (ahora mismo la 0.2.0 en desarrollo). Pero de cara a subirlo a pypi la versión no puede ser la misma, hay que añadirle apellidos, por ejemplo 0.1.1-dev1. Es la generación de ese apellido la que todavía no tengo bien resuelta.

Por cierto, no he dicho qué hace el paquete. Lo quiero utilizar para tener ordenadas implementaciones de algoritmos que utilizo para resolver algún problema. Ahora mismo tiene dos: un interpolador de curvas basado en [splines](https://es.wikipedia.org/wiki/Spline) y una trasnformación muy útil para modelos binarios, el [WoE (peso de la evidencia)](https://medium.com/@sundarstyles89/weight-of-evidence-and-information-value-using-python-6f05072e83eb). Mi implementación del WoE es más elegante que la del link que pongo, la de los splines de momento no tanto.

Finalmente, dejo aquí unos enlaces que he leído para poder hacer esto:

- [Una guía de cómo hacerlo de principio a fin](https://ron.sh/how-to-submit-a-package-to-pypi/)
- [Consideraciones para subir un paquete a pypi](https://medium.com/@joel.barmettler/how-to-upload-your-python-package-to-pypi-65edc5fe9c56)
- Tendría que firmar las tags de los repositorios, [aquí se explica por qué](https://rem.co/blog/2015/02/12/git-the-difference-between-lightweight-and-annotated-tags/)


