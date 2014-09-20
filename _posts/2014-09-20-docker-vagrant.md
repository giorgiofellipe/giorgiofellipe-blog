---
layout: post
title: Docker ou Vagrant
categories: [comparação, docker, vagrant]
tags: [comparação, docker, vagrant, virtualização, linux, lxc, container, devops]
description: O que são? Vantagens, desvantegens e aplicação de cada um deles
---

Com a popularização da computação em nuvem houve um aumento considerável na quantidade de máquinas virtuais que os administradores têm de manter. A criação e manutenção de uma máquina virtual (em virtualizadores como o Virtual Box, VMWare, etc) demanda grande quantidade de tempo e, por vezes, é complexa. Além do fato dessas máquinas virutais consumirem uma quantidade imensa de espaço em disco.

Devido a este crescimento e grande dificuldade ao operar surgiu a necessidade de melhorar esse modelo. Eis que um gênio observou que, era recreado toda configuração da máquina, incluindo HD, processadores virtuais e interfaces de rede, e ainda instalando o SO inteiro, quando na verdade o necessário seria somente utilizar um SO diferente como plataforma e alguns aplicativos diferentes. Sendo assim as novidades convergiram entre duas frentes distintas onde duas diferentes soluções se destacaram e serão melhor explicadas neste.

![Docker ou Vagrant]({{ site.url }}/assets/media/docker-vagrant.png)  

O que são?
-----

###Docker
É uma plataforma aberta para desenvolvedores e administradores de sistemas para construir, entregar e rodar aplicações distribuidas. É composto pelo Docker Engine, que é uma leve ferramenta de execução e empacotamento, e pelo Docker Hub, um serviço em nuvem responsável pelo compartilhamento de aplicações e automação de fluxos de trabalho. Ele permite que aplicações sejam rapidamente montadas e elimina o atrito e a diferença entre os ambientes de desenvolvimento, testes e produção, ou seja, sem essa de "na minha máquina funciona".  

Porém Docker não é uma ferramenta de virtualização de máquinas, ele é um ambiente de virtualização de Linux, construído sobre os LinuX Containers (LxC), que utiliza a funcionalidade cgroups para criar e rodar ambientes Linux virtuais isolados em um único host.  
Este VE (Virtual Environment - ambiente virtual) roda diretamente sobre o kernel já existente (do host) e apenas cria um container (recipiente) onde irão ser executados seus aplicativos, onde até é possível recriar o SO, já que este será apenas outro aplicativo rodando sobre o kernel.  

> Já estão, desde a versão 0.9, trabalhando para que o Docker não seja restrito apenas ao LxC, mas também compatível com KVM, Hyper-V, Xen, etc.

Uma desvantagem que vale se observar a respeito do docker é de que, pelo fato de compartilhar o kernel, seus containers não terão completo isolamento.

###Vagrant
Lançado em 2010, pode ser rapidamente resumido como um gerenciador de máquinas virtuais. Ele permite que você crie um script e empacote as configurações da máquina virtual. Sua proposta, assim como a do Docker, é acabar com a desculpa de que "na minha máquina funciona".  
Entretanto o Vagrant continua sendo uma máquina virtual, ainda que com muito mais recursos que as ferramentas comuns de virtualização. Por exemplo, talvez um dos recursos mais interessantes seja a possibilidade de integrá-lo com ferramentas de gestão de configuração (CM - Configuration Management), como Chef ou Puppet, para pré-configurar suas máquinas virtuais.

Como funcionam
-----

O que o Docker faz é permitir-lhe, por usar AuFS como sistema de arquivos, reutilizar "imagens" entre vários de seus containers, em outras palavras, enquanto com uma imagem de 1GB do seu SO gastaria 5GB para subir 5 VMs normais, com Docker você continuaria usando 1GB, talvez um pouco mais, devido ao fato das camadas poderem ser compartilhadas entre seus containers.

Algumas vantagens obtidas com a utilização do Docker:

* <strong>Containers fácilmente portáveis:</strong> você pode criar uma imagem de toda a configuração e aplicativos instalados em seu container, transferir e istalar em outro host com Docker previamente instalado.
* <strong>Versionamento:</strong> Docker permite que você versione as alterações de um container de uma forma muito semelhante ao git. Permitindo portanto verificar as diferenças entre versões, commitar novas versões e voltar (rollback) versões.
* <strong>Reutilização de componentes:</strong> como citado anteriormente as imagens criadas podem ser reutilizadas, vamos supor que diversas de suas aplicações utilizem um stack com Apache e MySQL, desta maneira você instala e configura ambos e cria uma imagem base, contendo estes itens, que representará a sua instalação e configuração, desta maneira esta imagem poderá ser reutilizada em quantos forem os containers que a necessite
* <strong>Compartilhamento:</strong> o Docker Hub, citado no incício, já está povoado de milhares de containers com as mais diversas aplicações instaladas e configurações aplicadas, desta maneira você pode rápidamente criar sua aplicação com uma base desenvolvida por outra pessoa, ou ainda criar sua base e compartilhá-la.

Por outro lado o Vagrant continua a criar máquinas virtuais, ainda que mais leves e com mais recursos que as tradicionais. Vagrant permite que estas VMs sejam reproduzidas utilizando VirutalBox, VMWare ou AWS.

Quando utilizar um, outro ou ambos
-----

###Quando usar o Docker

* Como sistema de controle de versão do SO inteiro de sua aplicação
* Quando você deseja distribuir (ou colaborar) o SO de sua aplicação com uma equipe
* Para executar em seu computador a aplicação com o mesmo ambiente do servidor em que a mesma encontra-se em produção
* Sempre que sua aplicação necessite de várias etapas de desenvolvimento (desenvolvimento, testes, qualidade, produção)

###Quando usar o Vagrant

Basicamente nas mesmas situações do Docker, exceto pelo fato do versionamento e colaboração, portanto:

* Para executar em seu computador a aplicação com o mesmo ambiente do servidor em que a mesma encontra-se em produção
* Sempre que sua aplicação necessite de várias etapas de desenvolvimento (desenvolvimento, testes, qualidade, produção)
* Quando sua equipe trabalha com poucas aplicações/projetos simultâneos

###Concluindo
Ainda que pareçam competir entre si alguns adminsitradores conseguiram unir as duas tencnologais a modo de complementarem-se. 

Em determinado cenário temos a seguinte situação: Vagrant é utilizado para criar a máquina virtual base, então quando necessitar criar configurações distintas, mas que continuem utilizando esta base, utilize o Docker para pré-configurar e criar versões leves desta base. 

> Tal discussão pode ser acompanhada através deste <a href="http://stackoverflow.com/questions/16047306/how-is-docker-io-different-from-a-normal-virtual-machine?rq=1">link</a>

Se você necessita de um isolamento entre as aplicações e necessida criar diversos ambientes diferentes, então Docker é o caminho! Já se você necessita de isolamento total vá de Vagrant!

Abaixo uma tabela que pode ajudar a você DevOps a decidir qual utilizar:

|Recurso 										| | | | | |Docker 		| | | | | |Vagrant 										|
|-----------------------------------------------|-|-|-|-|-|-------------|-|-|-|-|-|---------------------------------------------|
|Tipo de virtualização 							| | | | | |VE			| | | | | |VM 											|
|Garantia de recursos a nível de hardware 		| | | | | |Não			| | | | | |Sim 											|
|Plataformas de SO suportadas 					| | | | | |Somente Linux| | | | | |Linux, Unix, Windows 						|
|Tempo de inicialização 						| | | | | |Segundos		| | | | | |Alguns minutos 								|
|Nível de isolamento 							| | | | | |Parcial		| | | | | |Total 										|
|Tamanho dos sistemas virtuais 					| | | | | |Muito leve	| | | | | |Pesado 										|
|Extras 										| | | | | |Rápido, fácil| | | | | |Integração com CMs 							|

-

<p class="small"> 
Sintam-se a vontade para criticar, opinar e corrigir.
</p>
