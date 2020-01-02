# Angular CLI

O Angular CLI é uma ferramenta de linha de comando que você usa para inicializar, desenvolver e manter aplicações em Angular. Você pode usar a ferramente diretamente por um terminal de linha de comando, ou com uma interface gráfica interativa como o Angular Console, o qual não abordaremos nesse momento.

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

Na sequência o objetivo de cada parâmetro:

|Parâmetro|Descrição|
|---|---|
|minimal|Quando verdadeiro, cria um projeto sem nenhum framework de testes|
|skipGit|Quando verdadeiro, não inicializa um repositório git|
|skipTests|Quando verdadeiro, não gera arquivos "spec.ts" no novo projeto|
|skipInstall|Quando verdadeiro, após a criação do projeto não isntala as dependências NPM|

## Rodando a aplicação criada

Agora já temos o nosso projeto criado com uma estrutura simples, pronto para criarmos os nossos componentes, rotas, páginas e estilos, ou seja, construir a aplicação web que quisermos. Mas primeiro vamos instalar as dependências NPM especificadas no arquivo `package.json`. Para isso vamos rodar o romando que irá instalar as dependências.

A partir do diretório raíz do projeto criado, executar o comando:

```
npm install
```

Após a instalação das dependências, rodar o comando para inicializar um pequeno servidor HTML provido pelo próprio AngularCLI:

```
ng serve
```

Se tudo ocorrer com sucesso a aplicação estará disponibilizada no seguinte endereço: http://localhost:4200. A porta 4200 é a padrão mas pode ser mudada utilizando o argumento `--port=<port>`.

```
ng serve --port=8080
```

Pronto! A aplicação estará rodando agora na porta 8080: http://localhost:8080.

___

Para entendimento dos conceitos de uma aplicação em Angular pode acessar este link no qual é explicado os conceitos de componentes, templates, rotas, pipes e etc.