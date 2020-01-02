# Conceitos

- [NgModule](#ngmodule)
    - [Declarations](#declarations)
    - [Imports](#imports)
    - [Providers](#providers)
    - [Bootstrap](#bootstrap)
- [Component](#component)
    - [Comunicação entre componentes](#comunicação-entre-componentes)
        - [Input](#input)
        - [Output](#output)
- Routes

## NgModule

Um NgModule especifica como as partes de uma aplicação Angular se integram. Cada aplicação tem no mínimo um módulo Angular, o módulo principal that you bootstrap para executar a aplicação, por convensão, é chamado de AppModule.

Se você usar o Angular CLI para gerar a aplicação, o módulo principal AppModule pode ser ilustrado como:

```
/* JavaScript imports */
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

/* the AppModule class with the @NgModule decorator */
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Após as linhas de importação podemos ver a classe com a anotação @NgModule.

A anotação @NgModule identifica a classe AppModule como um NgModule. @NgModule recebe como parâmetro um objeto metadata que diz ao Angular como compilar e executar a aplicação.

### Declarations

A propriedade declarations do módulo diz ao Angular quais componentes pertencem ao módulo que o está declarando. Conforme você vai criando componentes, adicione-os na propriedade declarations.

Você deve declarar cada componente em no máximo uma classe NgModule. Se você usar o componente sem o declarar, o Angular irá lançar mensagens de erro.

A propriedade declarations apenas aceita "declaráveis". "Declaráveis" são componentes, diretivas e "pipes". Todos esses tipos de "declaráveis" devem estar especificados na propriedade declarations do módulo. "Declaráveis" devem pertencer a um módulo somente. O compilador emite erros se for tentado declarar uma mesma classe "declarável" em mais de um módulo.

**Essas classes declaradas ficam visiveis para todos os componentes do módulo mas invisiveis para componentes em outros módulos a não ser que as mesmas sejam exportadas no módulo e o módulo seja importado em outro módulo**.

Um exemplo de utilização da propriedade "declarations":

```
...
declarations: [
  YourComponent,
  YourPipe,
  YourDirective
],
...
```

Um "declarável" deve pertencer a somente um módulo, então só o declare em um @NgModule. Quando precisar adicionar em outro, importe o módulo em questão que possui o "declarável" declarado.

Apenas classes com a anotação @NgModule são especificadas na propriedade "imports".

### Imports

A propriedade "imports" aparece exclusivamente no objeto metadata da anotação @NgModule. Ela diz ao Angular sobre os outros módulos que o módulo em questão precisa para funcionar.

Os módulos especificados nessa propriedade são os módulos que exportam componentes, diretivas ou "pipes" que templates de componentes do módulo que os declaram, referenciam. Um exemplo é o caso do componente AppComponent, o qual referencia componentes, diretivas, ou "pipes" dos módulos BrowserModule, FormsModule, ou HttpClientModule. Um template de componente pode referenciar um componente, diretiva, ou "pipe" quando a classe referenciada é declarada no módulo que o referencia ou quando a classe é importada a partir de outro módulo.

### Providers

A propriedade "providers" é onde se declara as "services" que a aplicação precisa. Quando é declarado as "services" nesta propriedade elas estão disponíveis para toda a aplicação. As "services" são classes que possuem a anotação @Injectable os quais possuem métodos com lógicas de negócios e de busca de dados a um back-end.

### Bootstrap

A aplicação Angular se inicia a partir de um processo chamado "bootstraping" a partir do ponto de entrada que é também conhecido como entryComponent. Além de realizar outras funções, o processo de inicialização cria os componentes declarados na propriedade e insere cada um dele no DOM do navegador.

Cada componente criado e inicializado possui sua própria árvore de componentes. Inserindo um componente criado e inicializado geralmente dispara um processo em cascata de criação de componentes que formam a árvore.

Você pode até declarar mais de uma árvore de componentes na sua página, mas a maioria das aplicações possuirá apenas uma árvore de componentes que será inicializada a partir do componente principal ou raíz.

Esse componente raíz é geralmente chamado AppComponent e é ele que declaramos na propriedade "bootstrap".

O processo de "bootstraping" pode ser observado no código abaixo, geralmente declarado no arquivo `main.ts`.

```
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

## Component

Componentes são classes com a anotação @Component que atuam como controles de telas possuindo propriedades que armazenam dados fornecidos pelo usuário através de formulários ou fornecidos através de integração com serviços remotos. Possuem métodos que realizam ações a partir de interações do usuário com a tela, como cliques de botão, preenchimento de campo e etc. 

Os conteúdos das propriedades são exibidos na tela através de páginas HTML associadas ao componente.

Um componente pode ser uma página inteira em HTML de uma aplicação ou site ou uma pequena porção de HTML com objetivos muito específicos. A ideia principal dos componentes é que eles possam ser construídos para serem reutilizados por diversas partes da aplicação ou site.

### Comunicação entre componentes

#### Input

#### Output
