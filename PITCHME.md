# WEBPACK GUIDE

## URL para visualização

[https://gitpitch.com/tiagolpadua/webpack-guide/master](https://gitpitch.com/tiagolpadua/webpack-guide/master)

- TIAGO LAGE PAYNE DE PÁDUA

---

## O que é o Webpack?
Webpack é uma ferramenta de construção que coloca todos os seus ativos ("assets"), incluindo JavaScript, imagens, fontes e CSS em um grafo de dependências.
---
## Um pouco de história
<!--
    Antes das ferramentas de construção atuais que temos no JavaScript, era
    função do desenvolvedor incluir na página os scripts que eram necessários,
    assim como controlar a ordem de carregamento dos mesmos, veja esse exemplo de
    html:
-->
---
## Vanilla
```html
<!-- index.html -->
<html>
<head>
    <title>Minha Página</title>
    <script src="jquery.min.js"></script>
    <script src="jquery.some.plugin.js"></script>
    <script src="main.js"></script>
</head>
<body>
    <h1>Olá Mundo!</h1>
</body>
</html>
```
```js
//main.js
$(document).ready(function () {
    window.alert('Hello World!');
});
```
---
<!-- Com a chegada das ferramentas de build como o grunt e o gulp, passou-se a ser criado um bundle -->
## Grunt / Gulp
```html
<!-- index.html -->
<html>
<head>
    <title>Minha Página</title>
    <script src="bundle.js"></script>
</head>
<body>
    <h1>Olá Mundo!</h1>
</body>
</html>
```
```js
//build-script.js
var scripts = [  
    'jquery.min.js',
    'jquery.some.plugin.js',
    'main.js'
].concat().uglify().writeTo('bundle.js');
```
---
## Browserify
```js
// main.js
'use strict';

var R = require('ramda');

var square = function square (x) { return x * x; }  
var squares = R.chain(square, [1, 2, 3, 4, 5]); 

document.getElementById('response').innerHTML = squares;
```
<!--
No entanto, mesmo com as ferramentas de build, cabia ao desenvolvedor ajustar a ordem e declarar explicitamente quais arquivos eram necessários

Após esta fase, o JavaScript passou a permitir a criação de módulos, utilizando os comandos "require" e "module.exports", no entanto, os navegadores ainda não dão suporte a esta sintaxe. É aí que entra o Browserify, que transforma os códigos de require em algo que o navegador possa processar

Mas se o Browserify já resolve este problema, poquê precisamos do Webpack?

O Webpack dá um passo a mais, ele permite que você faça "require" em ativos estáticos, como arquivos de imagem e CSS, não só em arquivos JavaScript como o Browserify:
-->
---
## Webpack
```js
import _ from 'lodash';
import './style.css';
import Icon from './icon.png';
import Data from './data.xml';

function component() {
    var element = document.createElement('div');

    // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    element.classList.add('hello');

    // Add the image to our existing div.
    var myIcon = new Image();
    myIcon.src = Icon;

    element.appendChild(myIcon);

    console.log(Data);

    return element;
}

document.body.appendChild(component());
```