---
title: "Usando vim"
slug: usando-vim
date: 2019-07-02T22:33:19+02:00
draft: false
tags: [vim, hugo]
---

El ratón es lo más cómodo pero el teclado es lo más rápido. Por eso quiero usar vim más en la medida de lo posible. Por ejemplo para bloguear. En [Hugo](https://gohugo.io/) se puede [crear un post con el comando *hugo new posts/un-post-nuevo.md*](https://gohugo.io/getting-started/quick-start/) y, para hacerlo más cómodo se puede añadir la línea 
```toml
NewContentEditor = "vim"
```
al *config.toml* de modo que al escribir ese comando se abra vim. Lo cuentan [aquí](https://discourse.gohugo.io/t/create-and-open-new-post-with-one-liner-in-terminal/1454/2)

Y con eso es suficiente par empezar a trabajar. Parece más rápido que usar mi adorado [Visual Studio Code](https://code.visualstudio.com/), que es el editor que realmente uso. Pero siempre viene ver saber usar vim porque es lo que está disponible en entornos Linux a los que se suele conectar uno por ssh.

## Algunos trucos de vim
- la letra *o* inserta una línea debajo del cursor. En mayúscula lo hace encima. [Editando el .vimrc se pueden hacer cosas más complejas](https://vim.fandom.com/wiki/Quickly_adding_and_deleting_empty_lines).
- normalmente el cursor se desplaza por líneas físicas, no por líneas mostradas, [eso también se puede cambiar](https://vim.fandom.com/wiki/Move_cursor_by_display_lines_when_wrapping).
 
## Plugins
Vim tiene plugins y no hay un sistema único para gestionarlos. Al fin y al cabo los plugins no son más que scripts que se llaman desde el .vmrc, donde se puede configurar todo.

Yo utilizo [plug.vim](https://github.com/junegunn/vim-plug) porque lo recomienda [este señor](https://www.youtube.com/watch?v=cTBgtN-s2Zw)
