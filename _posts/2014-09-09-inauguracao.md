---
layout: post
title: Inauguração - Como criar um blog como este
categories: [tutorial, jekyll]
tags: [tutorial, criar, jekyll, blog, github, poole]
description: Bem-vindo! Aprenda como criar um blog como este, utilizando Jekyll + GitHub Pages
---

Hail!
-----

Este é o post inaugural do meu blog, decidi começá-lo há tempo porém somente agora tomei coragem e vergonha na cara para botar a mão na massa e botar a ideia pra funcionar.  
Bom, neste blog trarei algumas <strong>experiências</strong> minhas como desenvolvedor, em alguns <strong>projetos</strong> que já participei ou estou participando, falarei também sobre <strong>novidades</strong>, farei também alguns <strong>tutoriais</strong>, algo como um self-reminder a princípio mas que será lapidado conforme eu for ganhando prática nesta <strong>arte de blogar</strong>.

Espero que gostem!



-----

Tá na hora de me apresentar!  
-----
Pra quem não me conhece aqui vai uma mini-bio:  
Meu nome é <strong>Giorgio Fellipe</strong>, tenho 20 anos, sou natural de Lages - SC, moro em Rio do Sul - SC há aproximadamente 12 anos.  
Sou solteiro, aquariano, vascaíno, metido e orgulhoso.  
Sou desenvolvedor de softwares desde 2011, já desenvolvi utilizando as linguagens <strong>COBOL, Java, PHP e JS</strong>. Atualmente estou focando meus estudos em <strong>tecnologias front-end</strong>, como <strong>AngularJS</strong>, por exemplo.

-----

Para que este post não seja nulo, sem conteúdo, irei fazer um breve tutorial de como montar um blog como este.

##Como criar um Blog - Jekyll (poole) + GitHub!
![Jekyll]({{ site.url }}/assets/media/jekyll-logo.png)

###O que é Jekyll?

Podemos definir Jekyll como um gerador de sites estáticos. Seu principal objetivo é tornar estes sites mais leves e menos suscetíveis a falhas. Ele é baseado em diversos padrões de formatação de textos e blog posts, como Markdown. Utiliza um padrão de templates chamado Liquid, que utiliza YAML para exibir e armazenar valores de variáveis.  

####Poole

<a href="https://github.com/poole/poole">Poole</a> é um boilerplate para iniciar e entender o Jekyll mais rápido, fornece uma estrutura pronta e posts de exemplo que você pode se basear e criar seus próprios.

###Como o Jekyll funciona?

Parece complicado, mas na verdade o que ele é faz é com que você escreva seu post em um formato bem difundido na WEB, o Markdown (formato ".md"), que posteriormente é interpretado e convertido como uma página HTML pelo Jekyll. Quando "iniciado" o Jekyll lê todas as páginas e posts e gera uma pasta (_site) com todo o conteúdo estático.

###Estrutura de pastas

![Estrutura de Pastas]({{ site.url }}/assets/media/directories.png)  

Existem algumas pastas padrões, elas são precedidas por um underline (_).

<strong>_includes</strong> - é a pasta onde ficam páginas com trechos que são bastante utilizados ao longo do projeto, como por exemplo o cabeçalho e o rodapé do blog.  
<strong>_layouts</strong> - como o nome sugere é a pasta onde ficam os arquivos de layout das páginas a serem acessadas ao longo do blog, onde por exemplo, é definida a estrutura de post, a estrutura da visualização do seu perfil, etc. Dentro destas são feitas as chamadas de conteúdo.  

Estas são as padrões, porém você pode organizar seu projeto com outras pastas. Ao gerar o conteúdo estático o Jekyll copia todas as pastas do projeto não precedidas por um underline (_), estas são ignoradas na geração do código final.

###Mãos a massa

Li bastante sobre Jekyll antes de começar a colocar a mão e fazer funcionar. Admito que nem sempre sou assim, mas com experiências recentes aprendi que todo tempo gasto estudando algo que você deseja fazer será recuperado ao colocar em prática.  
Enfim, a maneira mais rápida de colocar um blog como este em produção é utilizando o <a href="https://github.com/poole/poole">poole</a>.

> Antes de mais nada, você deverá ter Ruby instalado em sua máquina.  
Partirei do pressuposto que você já o possui.

Para usuários de Macs ou Linux é simples, basta digitar o seguinte em seu terminal:  
{% highlight bash %}
$ gem install jekyll
{% endhighlight %}


> Se você utiliza <strong>windows</strong> há um <a href="http://jekyll-windows.juthilo.com">tutorial</a> escrito por <a href="https://twitter.com/juthilo">@juthilo</a> que explica como instalar.

Para hospedar seu blog no GitHub basta fazer um fork do projeto <a href="https://github.com/poole/poole">poole</a> e criar o branch gh-pages deste repositório com todo o conteúdo neste branch.  
Se você está utilizando um domínio próprio modifique o arquivo CNAME e aponte para seu domínio. Nome meu caso: `blog.giorgiofellipe.com.br`  
Neste caso deverá ser adicionado ao seu DNS um registro CNAME com o prefixo desejado, no meu caso "blog".  

Caso você não esteja utilizando um domínio próprio deverá alterar o arquivo _config.yml, modificando o valor da variável baseurl para que a mesma seja apontada a URL do seu GitHub Pages. Por exemplo para o repositório github.com/username/repositoryname utilize http://username.github.io/repositoryname/ (não esqueça a barra ao final)  
Já no arquivo CNAME deve conter o seguinte: `username.github.io`

Pronto!
-----
Você já estará com seu blog online!


###Dicas

* No site <a href="http://jekyllthemes.org">Jekyll Themes</a> existem diversos temas para Jekyll site.
* Leia a documentação no <a href="http://jekyllrb.com">site oficial</a>.
* Sinta-se a vontade para me perguntar e pratique! ;)