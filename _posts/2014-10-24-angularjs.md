---
layout: post
title: AngularJS para jQuery users
categories: [tutorial, angularjs]
tags: [tutorial, angularjs]
description: Uma introdução ao AngularJS, comparando-o com jQuery
---
http://www.artandlogic.com/blog/2013/03/angularjs-for-jquery-developers/

#####Buenas!

Neste post irei fazer uma introdução à framework JavaScript da moda: [AngularJS](https://angularjs.org/), mantida pelo Google.  

A abordagem será uma comparação à biblioteca jQuery, porém, veja bem, são tipos de ferramentas diferentes. jQuery é uma biblioteca, já AngularJS é uma framework. Ao utilizar uma biblioteca seu código decide quando realizar a chamada de determinada função da biblioteca, quando utilizando uma framework você implementa callbacks e a framework decidirá quando chamá-los.

Fica mais fácil de entender tal diferença quando pensamos no que está acontecendo em tempo de execução. Com jQuery nada acontece em "background", qualquer execução de código jQuery é disparado por uma trigger vinculada ao DOM.  
Já o Angular torna sua árvore DOM e seu javascript em um aplicativo Angular. O HTML com as diretivas do Angular é compilado em uma árvore de views, os scopes e controllers são vinculados às views, e existe um loop interno na aplicação responsável por garantir a sincronização de dados (data binding) entre a view e o model. Ou seja, temos uma aplicação MVC.

#[![AngularJS](https://angularjs.org/img/AngularJS-large.png)](https://angularjs.org/)  

###Declarativa e não imperativa

Diferente de outras frameworks ou bibliotecas o Angular não trata o HTML ou JavaScript como um bug a ser corrigido. Invés disso ele os utiliza de uma maneira que fará você se perguntar "como que eu não pensei nisso antes?". Veja o exemplo abaixo:

Imaginemos que queremos mostrar e esconder um elemento com base no status (checked/unchecked) de um checkbox na tela.  
Utilizando jQuery teriamos algo como o seguinte:

```
<input id="toggleStatus" type="checkbox">
<div id="elementTarget">
    Este elemento aparecerá e desaparecerá conforme o estado do checkbox!
</div>
<script>
    $(function() {
         function toggle() {
            var isChecked = $('#toggleStatus').is(':checked');
            var elementTarget = $('#elementTarget');
            if (isChecked) {
                elementTarget.show();
            } else {
                elementTarget.hide();
            }
        }
        $('#toggleStatus').change(function() {
            toggle();
        });
        toggle();
    });
</script>
```

Repare que o jQuery trata o DOM de forma imperativa, pegue esse nó, pegue aquele atributo, valida valor do atributo, faz isso, faz aquilo.  
Com o mesmo objetivo teríamos o seguinte se utilizando Angular:

```
<input ng-model="elementTarget" type="checkbox">
<div ng-show="elementTarget">
    Este elemento aparecerá e desaparecerá conforme o estado do checkbox!
</div>
```

É isso! Nada de código JavaScript, somente uma forma fácil e limpa de declaração dos binds & rules específicos.

> Veja este exemplo funcionando [aqui](http://jsfiddle.net/Y2M3r/1094/).

###Two-Way Data Binding

Esta técnica consiste em manter em sincronia os valores do modelo com os valores da view, ou seja, qualquer alteração na view será automáticamente refletida no modelo e qualquer alteração no modelo será propagada para a view.  
Utilizando isto temos uma vantagem enorme, sendo que o modelo será então o que no Angular é chamado de "single-source-of-truth" (única fonte da verdade), simplificando portanto o modelo de desenvolvimento, interpretando a view como mera projeção do seu modelo.

![Two-Way Data Binding](https://docs.angularjs.org/img/Two_Way_Data_Binding.png)

###Injeção de Dependências

O Angular é tido como uma das ferramentas que possui a melhor e mais elegante maneira de trabalhar com dependências.  
