---
layout: post
title: AngularJS para desenvolvedores jQuery
categories: [tutorial, angularjs, javascript]
tags: [tutorial, angularjs, framework, javascript, jquery]
description: Uma introdução ao AngularJS, comparando-o com jQuery
---

#####Buenas!

Neste post irei fazer uma introdução à framework JavaScript da moda: [AngularJS](https://angularjs.org/), mantida pelo Google.  
Este post é uma tradução e adaptação do [post de Vlad Orlenko](http://www.artandlogic.com/blog/2013/03/angularjs-for-jquery-developers/) publicado em 6 de março de 2014.

#[![AngularJS]({{ site.url }}/assets/media/angularjs.png)](https://angularjs.org/)  

A abordagem será uma comparação à biblioteca jQuery, porém, veja bem, são tipos de ferramentas diferentes. jQuery é uma biblioteca, já AngularJS é uma framework. Ao utilizar uma biblioteca seu código decide quando realizar a chamada de determinada função da biblioteca, quando utilizando uma framework você implementa callbacks e a framework decidirá quando chamá-los.

Fica mais fácil de entender tal diferença quando pensamos no que está acontecendo em tempo de execução. Com jQuery nada acontece em "background", qualquer execução de código jQuery é disparado por uma trigger vinculada ao DOM.  
Já o Angular torna sua árvore DOM e seu javascript em um aplicativo Angular. O HTML com as diretivas do Angular é compilado em uma árvore de views, os scopes e controllers são vinculados às views, e existe um loop interno na aplicação responsável por garantir a sincronização de dados (data binding) entre a view e o model. Ou seja, temos uma aplicação MVC.

###Declarativa e não imperativa

Diferente de outras frameworks ou bibliotecas o Angular não trata o HTML ou JavaScript como um bug a ser corrigido. Invés disso ele os utiliza de uma maneira que fará você se perguntar "como que eu não pensei nisso antes?". Veja o exemplo abaixo:

Imaginemos que queremos mostrar e esconder um elemento com base no status (checked/unchecked) de um checkbox na tela.  
Utilizando jQuery teriamos algo como o seguinte:

{% highlight HTML %}
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
{% endhighlight %}

Repare que o jQuery trata o DOM de forma imperativa, pegue esse nó, pegue aquele atributo, valida valor do atributo, faz isso, faz aquilo.  
Com o mesmo objetivo teríamos o seguinte se utilizando Angular:

{% highlight HTML %}
<input ng-model="elementTarget" type="checkbox">
<div ng-show="elementTarget">
    Este elemento aparecerá e desaparecerá conforme o estado do checkbox!
</div>
{% endhighlight %}

É isso! Nada de código JavaScript, somente uma forma fácil e limpa de declaração dos binds & rules específicos.

> Veja este exemplo funcionando [aqui](http://jsfiddle.net/Y2M3r/1094/).

###Two-Way Data Binding

Esta técnica consiste em manter em sincronia os valores do modelo com os valores da view, ou seja, qualquer alteração na view será automáticamente refletida no modelo e qualquer alteração no modelo será propagada para a view.  
Utilizando isto temos uma vantagem enorme, sendo que o modelo será então o que no Angular é chamado de "single-source-of-truth" (única fonte da verdade), simplificando portanto o modelo de desenvolvimento, interpretando a view como mera projeção do seu modelo.

![Two-Way Data Binding]({{ site.url }}/assets/media/two-way_data_binding.png)

###Injeção de Dependências

O Angular é tido como uma das ferramentas que possui a melhor e mais elegante maneira de trabalhar com dependências. Dependências são passadas a componentes quando necessário.

{% highlight JS %}
DataSource = $resource(url, default_params, method_details)
{% endhighlight %}

Digamos que você possui uma origem de dados JSON relacionado ao $resource no Angular (exemplo acima).  
Qualquer controller que necessitar de dados desta origem bastará incluir o DataSource como um dos parâmetros esperados e então a dependência será injetada automaticamente neste controller.  
Se você precisar fazer requisições HTTP assíncronas em seu controller, por exemplo, basta adicionar $http nos parâmetros.  
Precisar expor log ao console? Inclua $log nos parâmetros do controller.

O que acontece internamente no Angular é o seguinte: ele analisa o código de suas funções, identifica os parâmetros e faz a injeção dos services que seu código necessita.

###Acesso a Dados

Enquanto o Angular lhe dá a liberdade de estruturar sua camada Model como quiser, ele oferece uma maneira conveniente de conversar com APIs REST. Por exemplo, abaixo está uma maneira que podemos definir e usar para recuperar e salvar um User.

{% highlight JS %}
var User = $resource('/user/:userId', {userId:'@id'});
var user = User.get({userId:123}, function() {
  user.abc = true;
  user.$save();
});
{% endhighlight %}

Angular pré-define padrões para os métodos get, set, delete e também para a busca de registros, mas uma URL parametrizada lhe dá a oportunidade de customizar o acesso aos dados conforme suas necessidades.

Há diversas outras coisas que merecem ser mencionadas porém não foram: validação de formulário, teste unitário e a biblioteca angular-ui.

Vídeo de um screencast do Willian Oliveira mostrando na prática a criação de um app simples. Neste exemplo ele mostra sobre o Two-Way Data Binding, Diretivas e Injeção de Dependências.  

<iframe width="420" height="315" src="//www.youtube.com/embed/aICbo3f5wzY" frameborder="0" allowfullscreen></iframe>


Leitura recomendada: [ótima introdução ao AngularJS](http://javascriptbrasil.com/2013/10/18/guia-definitivo-para-aprender-angularjs-em-um-dia/).