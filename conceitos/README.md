# Conceitos

- [NgModule](#ngmodule)
    - [Declarations](#declarations)
    - [Imports](#imports)
    - [Providers](#providers)
    - [Boostrap](#bootstrap)

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
### Providers
### Bootstrap
