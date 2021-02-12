---
title: "Nueva Oportunidad a Vim"
date: 2021-02-10T14:07:38+01:00
draft: false
tags: ["vim", "productividad", "software"]
---
Recientemente le he dado una [nueva oportunidad a Vim](link a mí mismo) como editor. Ando aprendiendo Rust y he visto trabajar a Jon Genstedt, que hace sesiones de programación en directo en youtube y, además de la diferencia de conocimiento que tiene respecto a mí en Rust, utiliza de una forma muy rápida `neovim`.

En la Wikipedia se puede ver toda la historia de vi, vim y neovim. Son cada uno la evolución del anterior, aunque la compatibilidad es casi total. La diferencia práctica para mí parece está en los plugins, que es más fácil desarrollarlos para neovim. Aunque creo que me daría igual usar uno que otro, he decidido el más moderno, neovim.

No es para principiantes, pero si de verdad quieres que sea útil, lo importante son los plugins, que es con lo que se consigue tener vim al gusto de uno y que te dé la misma funcionalidad que `VsCode`. Los plugins y la configuración del vimrc (init.vim en el caso de neovim) son un mundo en sí mismo. A eso hay que añadirle además la memoria muscular para que los comandos y atajos de teclado salgan automáticamente, más allá insertar, borrar, guardar y cerrar (prácticamente todo lo que sabía hacer hasta ahora).

Cuento algunos problemas que tengo y cómo los he ido resolviendo:

# Ortografía

Hay una opción en vim, ```set spell```, que detecta errores ortográficos... en inglés. Para ponerlo en español hay que especificarlo: ```set spelllang=es_es```. Pero eso hay que hacerlo manualmente en cada archivo. Para detectar el idioma automáticamente hay un plugin que utiliza aspell (o el mucho peor hunspell), que no es el corrector ortográfico que utiliza vim por defecto. En cualquier caso, el plugin es:

```
Plug 'konfekt/vim-DetectSpellLang'
let g:detectspelllang_langs = {
      \ 'aspell'   : [ 'en_US', 'de_DE', 'es', 'it' ],
      \ }
```

Funciona bien, aunque todavía no tengo resuelto el que no aplique la corrección ortográfica en ciertas partes del archivo. En el markdown en el que edito este blog, la cabecera me gustaría omitirla. Investigaré.

# Completado de código

En este caso, sin hacer gran cosa, el plugin funciona directamente. Aunque reconozco que no sé muy bien quién es el encargado de qué:

```
Plug 'dense-analysis/ale'
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'racer-rust/vim-racer'
```
El caso es que funciona muy bien.

# Abrir archivos

Abro archivos desde el propio vim con una extensión que se llama CtrlP. Muy útil, funciona como VsCode.

```Plug 'ctrlpvim/ctrlp.vim'```

También hay otro que se llama ```fzf```, en teoría más útil porque puedes buscar dentro del texto de los archivos. Pero todavía no lo he probado.

# Buffers

Estoy acostumbrado a usar VsCode como bloc de notas informal en ficheros que dejo sin guardar. Lo primero que probé fue ```e <ARCHIVO>``` pero eso lo abre en la misma ventana y pierdes el actual. Eso creía hasta que [leí StackOverflow](https://vi.stackexchange.com/questions/8345/a-built-in-way-to-make-vim-open-a-new-buffer-with-file). Resulta que el buffer no se pierde, sólo hay que aprender a navegar por ellos.

Estoy en ello.

# Navegación por código 
Estoy acostumbrado, en cualquier IDE, a hacer click en el nombre de una función o de una variable y que me lleve al archivo donde se definió. Necesito de alguna forma configurar las tags a aprender el comando correspondiente, porque creo que con ```vim-racer```ya debería funcionar.

