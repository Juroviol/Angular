# Angular CLI

O Angular CLI é uma ferramenta de linha de comando que você usa para inicializar, desenvolver e manter aplicações em Angular. Você pode usar a ferramenta diretamente por um terminal de linha de comando, ou com uma interface gráfica interativa como o Angular Console, o qual não abordaremos nesse momento.

- [Pré-Requisitos](#pré-requisitos)
- [Instalando a ferramenta](#instalando-a-ferramenta)
- [Criando uma aplicação](#criando-uma-aplicação)
- [Rodando a aplicação criada](#rodando-a-aplicação-criada)
- [Realizando build da aplicação para deploy em ambiente produtivo](#realizando-build-da-aplicação-para-deploy-em-ambiente-produtivo)
- [Arquivos importantes](#arquivos-importantes)

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
|skipInstall|Quando verdadeiro, após a criação do projeto não instala as dependências NPM|

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

## Realizando build da aplicação para deploy em ambiente produtivo

Em [Rodando a aplicação criada](#rodando-a-aplicação-criada) nós vimos como inicializar um pequeno servidor HTML para conseguirmos visualizar nossa aplicação executando no navegador, no entanto para instalarmos nossa aplicação em algum servidor Web real é preciso que executamos um comando NPM para que a nossa aplicação possa ser montada de forma que esteja pronta para ser instalada. 

Como a nossa aplicação Angular é construída em fontes na linguagem TypeScript, precisamos de um procedimento que "traduza" esse fonte de TypeScript para JavaScript, uma vez que os navegadores, mesmos os mais modernos, não interpretam o TypeScript e sim JavaScript apenas. Dessa forma, a nossa aplicação, em sua forma original de construção, ou seja, com fontes TypesScript, não está preparada para rodar no navegador dos nossos usuários. 

Esse mesmo procedimento de "tradução" é realizado quando rodamos o comando `ng serve`, contudo o propósito deste comando é realizar os procedimentos necessários em contexto de **desenvolvimento** e disponibilizar um servidor HTML leve para visualizarmos a nossa aplicação. 

Portanto, para o propósito de disponibilizar a nossa aplicação em um servidor Web real (produtivo ou homologador por exemplo) utilizaremos o comando abaixo para que o Angular CLI possa realizar todos os procedimentos necessários para que a nossa aplicação esteja pronta para ser instalada em um servidor Web:

```
npm run build
```

O comando NPM acima irá executar o script que está especificado no arquivo `package.json`:

```
{
  ...
  "scripts": {
    ...
    "build": "ng build",
    ...
   }
   ...
 }
```

Basicamente nosso comando `npm run build` invoca o comando `ng build` do Angular CLI, o que esse comando faz está especificado em forma de configuração no arquivo `angular.json` que pode ser encontrado na raíz do nosso projeto recem criado. Mas de forma resumida: é realizado a "tradução" e a preparação dos arquivos de forma que eles contenham menos tamanho (para tornar mais performático) e que contenham o código ofuscado, para que os usuários não consigam entender o que a nossa aplicação faz.

Após toda a execução do processo, se tudo ocorrer com sucesso, é disponibilizado um diretório contendo todo a nossa aplicação traduzida, compactada e ofuscada. Esse diretório de saída está configurado também no arquivo `angular.json`, o qual, geralmente é chamado "dist". É os arquivos desse diretório que deverão ser instalados no servidor Web desejado.

## Arquivos importantes

O Angular CLI gera diversos arquivos, sendo alguns essenciais para a aplicação:

|Nome|Descrição|
|---|---|
|tsconfig.json|Contêm informações para a compilação do TypeScript para JavaScript. Podemos especificar nesse arquivos quais arquivos devem ser excluídos da compilação, qual a versão de JavaScript que queremos e etc.|
|package.json|Esse arquivo não está diretamente relacionado ao Angular, é nesse arquivo que especificamos as bibliotecas que nosso projeto irá utilizar. No caso, diversas bibliotecas angular. Mas podemos incluir novas bibliotecas de terceiros para agilizar a construção de nossa aplicação, como biblioteca de componentes visuais, por exemplo.|
|angular.json|Esse arquivo é utilizado pelo Angular CLI. Esse arquivo é diretamente ligado ao Angular CLI e sem ele nós não conseguimos utilizar a ferramenta para manter a nossa aplicação. É nesse arquivo que está especificado diversas configurações de como nossa aplicação será empacotada quando realizarmos o build. Antigamente o build das aplicações era feito com biblioteca de terceiros como grunt, gulp e webpack nos quais eram confifgurados diversos arquivos trazendo uma grande complexidade.

___

Para entendimento dos conceitos de uma aplicação em Angular pode acessar este link no qual é explicado os conceitos de componentes, templates, rotas, pipes e outras informações relevantes.
