---
layout: post
title: AngularJS para iniciantes
categories: [tutorial, angularjs]
tags: [tutorial, angularjs]
description: Uma introdução ao AngularJS, comparando-o com jQuery
---
http://www.artandlogic.com/blog/2013/03/angularjs-for-jquery-developers/

#####Buenas!

Neste post irei fazer uma introdução à framework JavaScript da moda: [AngularJS](https://angularjs.org/), mantida pelo Google.  

A abordagem será uma comparação à biblioteca jQuery, porém, veja bem, são tipos de ferramentas diferentes. jQuery é uma biblioteca, já AngularJS é uma framework. Ao utilizar uma biblioteca seu código decide quando realizar a chamada de determinada função da biblioteca, quando utilizando uma framework você implementa callbacks e a framework decidirá quando chamá-los.

Fica mais fácil de entender tal diferença quando pensamos no que está acontecendo em tempo de execução. Com jQuery nada acontece em "background", qualquer execução de código jQuery é disparado por uma trigger vinculada ao DOM.  
Já o Angular torna sua árvore DOM e seu javascript em um aplicativo Angular. O HTML com as diretivas do Angular é compilado em uma árvore de views, os scopes (veremos adiante) e controllers são vinculados às views, e existe um loop interno na aplicação responsável por garantir a sincronização de dados (data binding) entre a view e o model. Ou seja, temos uma aplicação MVC.

#[![AngularJS](https://angularjs.org/img/AngularJS-large.png)](https://angularjs.org/)  
