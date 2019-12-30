# Angular CLI

O Angular CLI é uma ferramenta de linha de comando que você usa para inicializar, desenvolver e manter aplicações em Angular. Você pode usar a ferramenta diretamente por um terminal de linha de comando, ou com uma interface gráfica interativa como o Angular Console, o qual não abordaremos nesse momento.

## Pré-Requisitos

- [NPM](https://nodejs.org/pt-br/download/)

## Instalando a ferramenta

A ferramente pode ser obtida e instalada utilizando o comando npm abaixo:

```
npm install -g @angular/cli
```

O comando irá instalar o pacote do Angular CLI globalmente para ser utilizado diretamente por linha de comando. 

## Criando uma aplicação

A documentação do Angular instrui, para criação de uma aplicação, a utilização do comando:

```
ng new <name>
```

Entretanto, a aplicação criada virá com diversas configurações e arquivos que não são necessários para nossa primeira aplicação, cujo objetivo principal é a aprendizagem.  

Dessa forma iremos utilizar o mesmo comando acima, porém passando alguns argumentos para dizer a ferramente que queremos uma estrutura de aplicação o mais simples possível.

```
ng new <name> --minimal=true --skipGit=true --skipTests=true --skipInstall=true
```





