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
### Imports
### Providers
### Bootstrap
