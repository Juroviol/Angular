# Conceitos

- [NgModule](#ngmodule)
    - [Metadata](#metadata-ngmodule)
        - [Declarations](#declarations)
        - [Imports](#imports)
        - [Providers](#providers)
        - [Bootstrap](#bootstrap)
        - [Exports](#exports)
- [Component](#component)
    - [Metadata](#metadata-component)
        - [Selector](#selector)
        - [Template](#template)
        - [Template URL](#template-url)
        - [Styles](#styles)
        - [Providers](#providers-component)
- [Data binding](#data-binding)
- [Comunicação entre componentes](#comunicação-entre-componentes)
    - [Input](#input)
    - [Output](#output)
- [Validação de formulários](#validação-de-formulários)
    - [Template driven](#template-driven)

## NgModule

Um NgModule especifica como as partes de uma aplicação Angular se integram. Cada aplicação tem no mínimo um módulo Angular, o módulo principal que você inicializa para executar a aplicação, por convensão, é chamado de AppModule.

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

### Metadata <a id="metadata-ngmodule"></a>

#### Declarations

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

#### Imports

A propriedade "imports" aparece exclusivamente no objeto metadata da anotação @NgModule. Ela diz ao Angular sobre os outros módulos que o módulo em questão precisa para funcionar.

Os módulos especificados nessa propriedade são os módulos que exportam componentes, diretivas ou "pipes" que templates de componentes do módulo que os declaram, referenciam. Um exemplo é o caso do componente AppComponent, o qual referencia componentes, diretivas, ou "pipes" dos módulos BrowserModule, FormsModule, ou HttpClientModule. Um template de componente pode referenciar um componente, diretiva, ou "pipe" quando a classe referenciada é declarada no módulo que o referencia ou quando a classe é importada a partir de outro módulo.

#### Providers

A propriedade "providers" é onde se declara as "services" que a aplicação precisa. Quando é declarado as "services" nesta propriedade elas estão disponíveis para toda a aplicação. As "services" são classes que possuem a anotação @Injectable os quais possuem métodos com lógicas de negócios e de busca de dados a um back-end.

#### Bootstrap

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

#### Exports

A propriedade define quais componentes, diretivas e pipes o módulo exporta de forma que outros módulos possam utilizar. Caso o módulo seja importado em outro módulo, e esse outro módulo utilize um componente, diretiva ou "pipe" sem que o módulo importado não os exporte, o Angular mostrará mensagens de erro.

Todo componente, diretiva e pipe exportado por um módulo precisa estar obrigatoriamente declarado na propriedade "declarations" deste mesmo módulo.

O objetivo de se exportar componentes, diretivas e "pipes" para outros módulos utilizarem, é para manter a estrutura da aplicação mais organizada de forma que esses códigos possam ser facilmente utilizado entre diversos módulos se for necessário posteriormente. 

Um bom exemplo é o [Angular Material](https://material.angular.io/), o qual nos disponibiliza diversos componentes já construídos com estilos do [Metarial Design](https://material.io/design/) para que possamos contruir a nossa aplicação de forma mais rápida, aproveitando esses componentes já construídos. Isso só é possível por que o Angular Material foi construído de forma a ser re-utilizado pela comunidade. Portanto é um módulo em Angular que declara na propriedade "exports" diversos componentes para que possamos utilizá-los. Pela internet encontraremos diversas bibliotecas do Angular que já foram construídas nos quais podemos usufruir para termos mais agilidade.

Abaixo podemos ver um componente que renderiza um simples texto na tela.

```
...
@Component({
    selector: "common-component",
    template: "<span>I'm common component!</span>"
})
export class CommonComponent {}
...
```

O componente criado é então declarado no módulo o qual pertence, conforme explicado no tópico [Componente](#component). O componente também é incluído na propriedade "exports" do módulo, pois queremos que esse componente possa ser utilizado por outro módulo.

```
...
@NgModule({
    imports: [BrowserModule, FormsModule],
    declarations: [CommonComponent],
    providers: [],
    exports: [CommonComponent]
})
export class CommonModule {}
...
```

No módulo o qual queremos utilizar o `CommonComponent` declaramos o seu módulo na propriedade "imports". Não há necessidade de declarar o `CommonComponent` na propriedade "declarations", pois essa propriedade serve para declarar apenas componentes, diretivas e "pipes" nativos do módulo, o qual não pertencem a outros módulos.  

```
...
@NgModule({
    imports: [BrowserModule, FormsModule, CommonModule],
    declarations: [AppComponent],
    providers: []
})
export class AppModule {}
...
```

Então no componente onde queremos utilizar o `CommonComponent` apenas o referenciamos.

```
...
@Component({
    selector: "app",
    template: "<common-component></common-component>"
})
export class AppComponent {}
...
```

## Component

Componentes são classes com a anotação @Component que atuam como controles de telas possuindo propriedades que armazenam dados fornecidos pelo usuário através de formulários ou fornecidos através de integração com serviços remotos. Possuem métodos que realizam ações a partir de interações do usuário com a tela, como cliques de botão, preenchimento de campo e etc. 

Os conteúdos das propriedades são exibidos na tela através de páginas HTML associadas ao componente.

Um componente pode ser uma página inteira em HTML de uma aplicação ou site ou uma pequena porção de HTML com objetivos muito específicos. 

A ideia principal dos componentes é que eles possam ser construídos para serem reutilizados por diversas partes da aplicação ou site.

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div>Hello World!</div>
  `,
  styles: []
})
export class AppComponent {
  title = 'myapp';
}
```

### Metadata <a id="metadata-component"></a>

#### Selector

Um seletor CSS que diz ao Angular para criar e inserir uma instância deste componente onde for encontrada a tag correspondente pelos templates HTML da aplicação. Por exemplo, se uma página HTML contém a tag `<app-hero-list></app-hero-list>`, então o Angular insere uma instância do componente correspondente entre as tags declaradas.

#### Template

O HTML que servirá como template para ser renderizado na tela onde o componente for referenciado. A especificação do HTML aqui se dá como uma string. No entanto é recomendável que se utilize a propriedade [templateURL](#template-url), pois divide as responsabilidades, tornando a aplicação mais organizada e modularizada.

#### Template URL

O endereço relativo ao componente onde se encontra o template HTML. Uma outra forma de prover um template de HTML é através da propriedade [template](#template), dessa forma o HTML pode ser especificado diretamente na propriedade não precisando criar um arquivo.

#### Styles

Para cada componente Angular criado, você pode definir não somente o template HTML, mas também os estilos CSS que estejam relacionados ao template, especificando seletores, regras e medias que for preciso.

A propriedade "styles" é uma maneira de contemplar isso. A propriedade recebe uma lista de "string" que contenham código CSS.

**Os estilos especificados no objeto metadata da anotação @Component se aplicam somente ao template do componente. Os estilos não reflitirão em componentes filhos ou em demais componentes irmãos ou pais**.

#### Providers <a id="providers-component"></a>

A propriedade especifica uma lista de services que o componente necessita. Nessa propriedade só pode ser especificado classes que sejam identificadas pela anotação @Injectable(). 

As services especificadas nessa propriedade, no contexto de componente, só estarão disponível para ser injetado no construtor desse componente, caso seja injetado no construtor de outro componente sem declará-lo na propriedade "providers" do componente em questão, o Angular lançará mensagem de erro. 

Para que uma service esteja disponível para ser injetado em qualquer componente, é preciso declará-lo na propriedade ["providers"](#providers-module) do módulo.

## Data binding

Sem um framework, você seria responsável por colocar os dados provenientes de serviços no HTML, controlar as atualizações desses dados e obter os dados a partir de ações dos usuários. Escrever código para controlar isso manualmente é tedioso, suscetível a erros e um pesadelo de entender como qualquer desenvolvedor experiente de front-end JavaScript pode afirmar.

Em simples palavras data binding é a "mágica" que faz com que os dados da tela sejam automaticamente alterados quando mudanças ocorrem em propriedades na memória do componente e que os dados em memória nos componentes sejam alterados a partir de ações do usuário, como preenchimento de formulário, por exemplo.

```
<li>{{hero.name}}</li>
<app-hero-detail [hero]="selectedHero"></app-hero-detail>
<li (click)="selectHero(hero)"></li>
```

- A interpolação `{{hero.name}}` renderiza a propriedade hero.nome do componente dentro da tag HTML `<li>`.
- O "binding" da propriedade `[hero]` passa o valor da propriedade selectedHero do componente pai para a propriedade hero do componente filho.
- O "binding" do evento `(click)` invoca o método selectHero do componente quando o usuário clica no nome do herói.

Data binding é importante não só para a comunicação entre template e componente como entre componentes pais e filhos.

### Two-way data binding

Two-way data binding (mais usado com formulários template-driven) combina "binding" de propriedade e evento em uma única notação. Abaixo um exemplo de utilização de two-way data binding com a diretiva ngModel.

```
<input [(ngModel)]="hero.name">
```

Com o two-way binding, o valor do dado da propriedade do componente reflete no input assim como o "binding" de propriedade acima mencionado. Porém nesse caso, as mudanças realizadas pelo usuário no campo refletem também na propriedade do componente, como acontece no "binding" de evento.

## Comunicação entre componentes

### Input

É possível passar informações entre componentes. Isso é possível criando um "canal" de recebimento de informação no componente o qual se deseje receber alguma informação. A informação pode ser qualquer tipo de dado, tanto dados primitivos, como textos, numeros, como também dados de objetos complexos.

Abaixo podemos ver um componente filho o qual quer receber informações de outros componentes que o referenciam em seus template de HTML. A viabilização de recebimento de uma informação de um outro componente se dá através da inclusão da anotação @Input() na propriedade o qual quer receber informação:

```
...
@Component({
    selector: 'child',
    template:'<span>{{informacao}}</span>'
})
export class Child {

    @Input()
    private informacao : string;

}
...
```

Na referencia do componente filho no componente pai é então passado o valor da propriedade `dado` do componente pai, cujo é inicializado com o valor: "uma informação importante!", para o componente filho através do "binding" de propriedade especificada pela notação `[informacao]="dado"`. Qualquer mudança na propriedade `dado` no componente pai, irá refletir automaticamente no componente filho. 

```
...
@Component({
    selector: 'parent',
    template: '<child [informacao]="dado"></child>'
})
export class Parent {

    private dado : string = "uma informação importante!";

}
...
```

### Output

Nos exemplos acima vimos como passar uma informação do componente pai para o componente filho utilizando o "binding" de propriedade. E quando precisamos passar alguma informação do componente filho para o pai? Nesse caso utilizaremos o "binding" de evento, no qual o pai ficará escutando por eventos emitidos pelo filho. 

Abaixo podemos ver o componente filho o qual renderiza através do template HTML um campo para preenchimento de texto. Para passar para o componente pai a informação que será digitada nesse campo: declaramos uma propriedade cuja classe é `EventEmitter` o qual possui um método `emit` que irá comunicar o componente pai que estará escutando por mudanças através do "binding" de evento. 

```
...
@Component({
    selector: 'child',
    template:'<input [(ngModel)]="informacao" (input)="inputChanged()"></span>'
})
export class Child {

    private informacao : string;

    @Output()
    private informacaoChange : EventEmitter<any> = new EventEmitter<any>();
    
    inputChanged() : void {
        this.informacaoChange.emit(this.informacao);
    }

}
...
```

Quando o campo é preenchido é invocado o método `inputChanged`, graças ao "binding" de evento `(input)` oferecido pelo próprio Angular nos campos HTML. Ao invocar o método `inputChanged` então invocamos o método `emit` da variável `inputChange` passando a informação armazenada na propriedade `informacao` o qual foi preenchida graças a diretiva `ngModel` do campo.

Na referência do componente filho no componente pai declaramos um "binding" de evento no evento anteriormente declarado no filho: `informacaoChange` com a anotação @Output. 

```
...
@Component({
    selector: 'parent',
    template: '<child (informacaoChange)="atualizarDado($event)"></child>'
})
export class Parent {

    private dado : string;
    
    atualizarDado(dado : string) : void {
        this.dado = dado;
    }

}
...
```

Quando o dado é preenchido no filho é então invocado o método `atualizarDado` do componente pai recebendo o valor e associando a propriedade `dado` do componente pai. 

Podemos modificar ainda no componente pai o nome do evento `(informacaoChange)` do "binding" de evento para apenas `(informacao)` pois o Angular sabe que toda variável declarada no componente do tipo `EventEmitter` e com a anotação @Output com o nome acrescido de "Change" pode ser referenciado apenas com o nome excluído da palavra "Change".  

```
...
@Component({
    selector: 'parent',
    template: '<child (informacao)="atualizarDado($event)"></child>'
})
export class Parent {

    private dado : string;
    
    atualizarDado(dado : string) : void {
        this.dado = dado;
    }

}
...
```

A modificação acima mencionada nos trás a possibilidade de termos o two-way binding na propriedade `dado` do componente pai, de forma que qualquer alteração na propriedade `dado` no componente pai, reflita na propriedade `informacao` do componente filho e vice-versa. Para isso precisamos voltar a incluir a anotação @Input na propriedade `informacao` do componente filho e remover o método `atualizarDado` do componente pai, para que possamos obter o two-way binding.

```
...
@Component({
    selector: 'child',
    template:'<input [(ngModel)]="informacao" (input)="inputChanged()"></span>'
})
export class Child {

    @Input()
    private informacao : string;

    @Output()
    private informacaoChange : EventEmitter<any> = new EventEmitter<any>();
    
    inputChanged() : void {
        this.informacaoChange.emit(this.informacao);
    }

}
...
```

```
...
@Component({
    selector: 'parent',
    template: '<child [(informacao)]="dado"></child>'
})
export class Parent {

    private dado : string;

}
...
```

## Validação de formulários

Em toda aplicação que possui formulários é preciso validar se os dados fornecidos pelos usuários estão de acordo com as regras que a aplicação espera que sejam contempladas. Em Angular, validar formulários é fácil, não sendo necessário a importação de bibliotecas de terceiros em JavaScript. Com o Angular conseguimos construir validadores baseados em regras customizadas além das que o próprio Angular nos provê. Existe ainda a possibilidade de construir validadores que interagem com webservices, onde a regra é processada em outra aplicação back-end.

### Template driven

A primeira forma de validação de formulários que vamos abordar é a "template driven form validation", o qual é a minha preferida. Nessa forma de validação nós separamos o código que irá validar os dados preenchido nos campos do código que ficará no nosso componente. Pois não queremos "poluir" nosso código do componente com diversos códigos contendo regras de validação de dados.

A separação do código responsável por validar dados de preenchimento é realizado através da utilização de [diretivas](#Diretivas).

Abaixo ilustrarei em código como utilizar validadores padrões e construir um validador customizado e um customizado e assíncrono com interação com webservice.

Abaixo temos nosso componente simples que contém apenas uma propriedade `cpf` e um método que será invocado quando clicarmos no botão "Salvar". 

```
...
@Component({
  selector: 'my-component'
  templateUrl:'template.html'
})
export class MyComponent {
    cpf: string;
    salvar() {}
}
...
```

No arquivo `template.html` referenciado na anotação @Component do nosso componente temos um campo de texto que irá receber os dados que serão colocados na propriedade `cpf`. 

```
<form (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" />
<button>Salvar</button>
</form>
```

Utilizando o atributo `required` do pŕoprio HTML, iremos dizer o Angular que esse campo é obrigatório.

```
<form (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required />
<button>Salvar</button>
</form>
```

Agora vamos colocar em pŕatica o conceito de template driven. Vamos criar uma varíavel `myForm` que receberá o objeto `NgForm` associado ao elemento `<form>` do nosso HTML. Nesse caso estamos pegando a instância deste objeto e guardando na nossa variável `myForm` que foi criada através da notação com `#` "hashtag". Com isso passaremos a ter acesso a diversas propriedades que o objeto do tipo `NgForm` oferece para referenciarmos no nosso próprio HTML.

```
<form #myForm="ngForm" (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required />
<button>Salvar</button>
</form>
```

Vamos colocar uma mensagem em um `span` para ser exibido quando o campo não for preenchido. Neste momento a mensagem sempre será exibida, independente de estar preenchido ou não.


```
<form #myForm="ngForm" (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required />
<span>Campo obrigatório.</span>
<button>Salvar</button>
</form>
```

Da mesma forma, iremos criar uma variável `cpf` que recebrá o objeto `NgModel` associado ao elemento `<input>` que possui a diretiva `ngModel`. Da mesma forma que no caso do form, teremos acesso a propriedades que o objeto do tipo `NgModel` oferece para referenciarmos no nosso próprio HTML a fim de controlarmos o melhor momento em que a mensagem de feedback deve ser exibida ao usuário.     

```
<form #myForm="ngForm" (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required #cpf="ngModel" />
<span>Campo obrigatório.</span>
<button>Salvar</button>
</form>
```

Agora que temos uma varíável que possui propriedades relativas ao estado de validação do campo, podemos utilizar destas propriedades para exibir a mensagem somente quando o campo estiver inválido. A propriedade que vamos utilizar é a `invalid` que nesse caso ao entrar na tela já estará inválido (por conta do atributo `required`) e a mensagem já será exibida, e não é esse o efeito que queremos. Sendo assim vamos prosseguir.

```
<form #myForm="ngForm" (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required #cpf="ngModel" />
<span *ngIf="cpf.invalid">Campo obrigatório.</span>
<button>Salvar</button>
</form>
```

Outra propriedade de estado do campo é a `touched` que ficará como verdadeiro quando o usuário focar no campo. Dessa forma a mensagem não será mais exibida quando entrarmos na tela, somente se caso o usuário tocar no campo.

```
<form #myForm="ngForm" (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required #cpf="ngModel" />
<span *ngIf="cpf.touched && cpf.invalid">Campo obrigatório.</span>
<button>Salvar</button>
</form>
```

Caso o usuário entre na tela e imediatamente clique no botão "Salvar" a mensagem não de erro não será exibida, pois estamos impondo a condição de que a mensagem só seja exibida caso ele tenha sido tocado e esteja inválido. Como o campo não terá sido tocado, a mensagem não será exibida. Portanto vamos adicionar mais uma verificação na nossa condição para que a mensagem seja exibida quando o formulário seja submetido também. Para isso vamos utilizar a propriedade `submitted` que está disponível na variável que declaramos anteriormente: `myForm`.

```
<form #myForm="ngForm" (submit)="salvar()">
<input type="text" name="cpf" [(ngModel)]="cpf" required #cpf="ngModel" />
<span *ngIf="(myForm.submitted || cpf.touched) && cpf.invalid">Campo obrigatório.</span>
<button>Salvar</button>
</form>
```

Agora vamos adicionar uma nova regra de validação para o formato do cpf preenchido. Já temos a regra de que o campo é obrigatório, graças ao atributo `required`. Para o formato do cpf vamos adicionar o atributo `pattern` que recebrá uma expressão regular.

```
<form #myForm="ngForm">
<input type="text" name="cpf" [(ngModel)]="cpf" required pattern="^\d{3}\d{3}\d{3}\d{2}$|^\d{3}.\d{3}.\d{3}-\d{2}$" #cpf="ngModel" />
<span *ngIf="(myForm.submitted || cpf.touched) && cpf.invalid">Campo obrigatório.</span>
</form>
```

Com a adição da nova regra, a mensagem de campo obrigatório será exibida quando preenchermos o campo com um formato inválido de CPF. Para resolver esse problema, ao invés de utilizar a expressão `cpf.invalid` na condição, iremos usar a expressão que se refere a invalidez pela regra de obrigatoriedade. O objeto do tipo `NgModel` possui uma propriedade chamada `errors` o qual é uma lista contendo os erros pelo qual o campo se tornou inválido. Dessa forma conseguimos saber por qual violação de regra o campo se tornou inválido.

Vamos então mudar a expressão: `cpf.invalid`, para `cpf.errors.required`, e para sabermos se o campo está inválido pela violação da regra de formato, a expressão: `cpf.errors.pattern`. 

```
<form #myForm="ngForm">
<input type="text" name="cpf" [(ngModel)]="cpf" required pattern="^\d{3}\d{3}\d{3}\d{2}$|^\d{3}.\d{3}.\d{3}-\d{2}$" #cpf="ngModel" />
<span *ngIf="(myForm.submitted || cpf.touched) && cpf.errors.required">Campo obrigatório.</span>
<span *ngIf="(myForm.submitted || cpf.touched) && cpf.errors.pattern">CPF inválido.</span>
</form>
```

### Reactive forms
