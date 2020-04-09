---
title: "Usando Git"
date: 2020-03-27T19:30:22+01:00
draft: false
tags: [git]
---

Además de los comandos básicos de git, cuando se trabaja con más personas se hace necesario no sólo el que todos los que trabajan en el equipo usen git sino acordar también la manera en la que se va a usar el repositorio. Esto es definir una manera de llamar las ramas y una política de ramificación (qué ramas se pueden crear a partir de otras) y qué tiene que pasar para poder integrar unas ramas en otras (```git merge```).

Hacer esto de manera estandarizada tiene dos ventajas. Por un lado se hace más fácil el integrar el código en procesos de integración y desarrollo continuos (las famosas *devops*). Y por otro, no menos importante, se elimina una barrera de entrada a la hora de incorporar nuevos miembros a los proyectos, pues es posible que ya conozcan el estándar.

Principalmente hay dos estándares, con sus pros y contras: [git-flow](https://nvie.com/posts/a-successful-git-branching-model/) y [github-flow](https://guides.github.com/introduction/flow/). Personalmente, en los proyectos empresariales suelo utilizar git-flow y en los personales github-flow. El motivo es que git-flow hace que sea más difícil que lleguen cosas sin probar a la rama master y esto es bueno en equipos donde hay desarrolladores con poca experiencia y desarrolladores que no son desarrolladores (lo segundo es bastante habitual).

Además ese motivo, git-flow es bueno cuando hay que llevar un control estricto de las versiones para lo cual recomiendo usar [*semver*, el nombrado semántico de versiones](https://semver.org/). Una cosa importante es usar siempre el flag *--no-ff* al integrar las ramas, la guía de git-flow lo menciona. Esto hace que cada vez que se hace un *merge* se cree un nuevo *commit* aunque no sea necesario porque podría haberse hecho sin él (con un *fast-forward*); en la práctica lo que se consigue es que en el dibujo de la historia del repositorio las ramas se vean con mucha más claridad y de forma explícita.

En esencia en git-flow todo el desarrollo ocurre en la rama *develop*. De la rama develop salen features (ramas con el prefijo *feature/*) y releases (ramas con el prefijo *release/*). A la rama *master* sólo se llevan los cambios de la rama *release*. En la rama *release* solo se pueden hacer correcciones de errores (*bugfix/*) y en la rama *master* sólo se pueden hacer *hotfix/*. Es habitual que la rama *release* se despliegue en un entorno de desarrollo o pruebas de usuario sobre el que se van corrigiendo errores y, una vez corregidos esos errores, se llevan (o no) a la rama *master*.

Github-flow es más fácil de usar. A partir de la rama *master* se crean ramas, con cualquier nombre. Cuando la rama está lista, se hace un *pull request* y entonces se hacen los cambios pertinentes. En github además se tiene una especie de wiki asociados a los *pull requests*, con lo cual se pueden discutir esos cambios. A partir de cualquier commit se puede hacer un despliegue. Una vez hechas las pruebas, el resultado es volver a *master* con *merge*. Y ya está.

Además (github-flow lo menciona pero no es imprescindible en su sistema) yo recomiendo hacer etiquetas con ```git tag``` para tener control de las versiones, es mucho más fácil referirse a un commit concreto por su etiqueta que por su commit.
