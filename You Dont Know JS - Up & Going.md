# You Don't Know JS - Up & Going

## Autor: Kyle Simpson
### Tradução: [Cezar Augusto](https://github.com/cezaraugusto/You-Dont-Know-JS)

## Capítulo 1 - Iniciando

### Código

#### Instruções
Grupo de pavalavras, números e operadores que realizam uma tarefa específica. Exemplo:
```js
a = b * 2;
```
Onde: 
- `a` e `b` são variáveis.
- `*` e `=` são operadores.

#### Expressão
Referência a qualquer valor ou varíavel (ou um conjunto delas combinados com operadores). No exemplo acima, a expressão `a = b * 2` é uma expressão de atribuição. Uma expressão mais comum é a *expressão de chamada*:
```js
alert (a);
```

#### Executando um programa:
A *engine* do JavaScript *compila* o programa no mesmo instante e imediatamente roda o código compilado. Então não é totalmente correto dizer que JavaScript é uma linguagem *interpretada*.

**Output:** no exemplo abaixo usamos o `console.log(..)` para imprimir texto (output). A parte do `log(b)` é usada como uma função de chamada (usar a variável `b` na função para pegar seu valor e imprimir no console). A parte do `console.` é uma referência ao objeto onde a função `log(..)`está localizada.

Exemplo:

```js
a = 21;
b = a * 2;
console.log( b );
```

**Input:** a mensagem a ser passada para o `prompt(..)`, neste caso, `"Please tell me your age:"`, é impresso no popup. Ao enviar a informação, o valor passado pelo usuário é armazenado em `age` e impresso.

```js 
age = prompt ("Please tell me your age:");
console.log(age);
```

#### Operadores
Será usado a palavra-chave `var` para declarar variáveis. A variável precisa ser declarada apenas uma vez para cada *escopo* e usada sempre que necessário.

Exemplo: 

```js
var a = 20;

a = a + 1;
a = a * 2;

console.log(a); //42
```


Podemos perceber o uso de operadores de:
- atribuição: `=`
- aritmético: `+`, `-`, `+`, `/`
- acesso a propriedade do objeto: `.` como em `console.log()`

####Valores e Tipos
Representações diferentes para os valores.
- valores primitivos: number, string e boolean.

#### Coerções entre Tipos
Caso seja necessário imprimir um número(`number`), é necessário converter o valor para `string`, em JavaScript isso é chamado `coerção`. 

Exemplo de coerção:

```js
var a = "42";
var b = Number( a );

console.log( a );   // "42"
console.log( b );   // 42
```

O `Number(..)` realiza uma coerção *explícita*. Em alguns casos o JavaScript realiza uma coerção *implícita*, exemplo: ao usar um operador de igualdade não-estrita para comparação (`"99.99" == 99.99`), o JavaScript converte o lado esquerdo para `number`, logo a comparação se torna verdadeira.

#### Variáveis
JavaScript é uma linguagem de tipagem diânimica (fraca), onde uma variável armazena valor de qualquer tipo.
- Propósito das variáveis: gerenciar o *estado* (acompanhamento das mudanças dos valores conforme seu programa está rodando) do programa.
- *Constante:* por convenção uma variável que não vai mudar de valor ao longo do programa, geralmente declarada no início do programa. Caso você tente alterar o seu lado após sua primeira declaração, o programa irá rejeitar a mudança. Na nova versão do JavaScript (ES6) constantes são declaradas usando `const` ao invés de `var`, exemplo:

    ```js
    // como em ES6:
    const TAX_RATE = 0.08;
    ```
    
####Condicionais
O JavaScript define uma lista de valores específicos que são considerados "falsos" (quando coergidos para boolean tornam-se false ou true), esses valores incluem 0 e "". Qualquer outro valor não incluído na lista de "falsos" será automaticamente definido como "verdadeiro" (true).

####Escopo
Coleção de variáveis e regras de como essas variáveis serão acessadas pelo nome. Exemplo: variáveis com o mesmo nome podem coexistir, mas apenas em escopos diferentes. Escopos podem ser aninhados, assim o código do escopo interno pode acessar o código do escopo externo.

## Capítulo 2 - Por dentro do JavaScript

### Valores e Tipos

JavaScript possui valores tipados. Os tipos nativos são: `string`, `number`, `boolean`, `null` e `undefined`, `object`, `symbol` (ES6).

- Bug JS: `typeof null` retorna um `"objeto"`.
- Uma variável pode chegar ao valor `undefined` de diversas maneiras, exemplo: funções que não retornam valores e o uso do operador `void`.

### Objetos
Valor composto onde pode ser definido propriedades que podem armazenar seus próprios valores de qualquer tipo.
- Podem ser acessados por *notação com ponto*: `obj.a`, quanto por *notação em colchetes*: `obj["a"]` (útil caso você tenha um nome com caracteres especiais).

#### Array
Um tipo `object` que armazena valores. A melhor maneira é utilizar arrays para valores posicionados numericamente e usar `object` para propriedades nomeadas.

#### Funções
Subtipo de `object`.

### Métodos de Tipos Nativos
Um valor `string` pode ser englobado por um objeto `String`, um `number` pode ser englobado por um objeto `Number`, e um `boolean` pode ser englobado por um objeto `Boolean`.

### Comparando Valores
Comparações utilizando igualdade ou desigualdade, onde o resultado é um `boolean`.

#### Coerção
Há dois tipos de coerção, *explícita* (ocorre através do código) e *implícita* (ocorre como efeito paralelo de outra operação). 
**Coerção explícita:**

```js
var a = "35";
var b = Number( a );

a; // "35"
b; // 35 -- o número!
```

**Coerção implícita:**
```js
var a = "35";
var b = a * 1; // "35" implicitamente coagido para 35 aqui

a; // "35"
b; // 35 -- o número!
```
#### Truthy & False
Quando um valor não-boolean é coagido para `boolean`, ele se torna `true` ou `false`. A lista dos que se tornam `false` é: 

- `""` (string vazia)
- `0`, `-0`, `NaN` (`number` inválido)
- `null`, `indefined`
-  `false`

Os demais valores se tornam  `true` quando coagidos.

#### Igualdade
Operadores de igualdade: `==`, `===`, `!=` e `!==`.

- `==` verifica igualdade de valor (uso da comparação: [link](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3));
- `===` verifica igualdade de valor e tipo (não permite coerção).

#### Desigualdade
Operadores de desigualdade: `>`, `<`, `>=` e `<=`.
- Se ambos os valores na comparação são `strings`, essa comparação então será feita lexicograficamente.
- Se um ou ambos os valores não forem `strings`, então ambos valores são coagidos para `number`.

### Variáveis
#### Escopos de Função
É usando a palavra-chave `var` para declarar a variável que irá referenciar o escopo da função corrente, ou escopo global.

#### Hoisting
É quando uma declaração `var` é elevada ao topo do escopo. Sua declaração é *hoisted*, mas não sua inicialização. 

#### Escopo Aninhado
Ao declarar uma variável, ele é disponibilizada em seu escopo e em escopos internos. 
- Caso tente setar uma variável que ainda não foi declarada, você irá gerar um erro ou criará uma variável no escopo global.
- ES6: ao usar a palavra-chave `let` a variável criada irá pertencer a um bloco individual.

#### Condicionais
Operador ternário (forma simplificada de if/else): 
```js
var a = 42;
var b = (a > 41) ? "hello" : "world";

// similar a:

// if (a > 41) {
// b = "hello";
// }
// else {
// b = "world";
// }

```

#### Modo Estrito (Strict Mode)
Determina regras rígidas para certos comportamentos. Faz o código se tornar mais seguro e com padrões mais definidos. O código também será melhor otimizado pelo *Motor*.

#### Funções como Valores
Exemplo:
```js
function foo() {
}
```
`foo` é uma variável que referência um escopo por onde é feita a referência para a função que está sendo declarada. A `function` por si só é um valor.
- A função pode receber valor como argumento e também pode por conta própria ser um valor.
Exemplo:
```js
var foo = function() {
};
var x = function foo() {
};
```

#### Expressões de Funções Invocadas Imediatamente (IIFEs)
É usando para executar uma expressão de função. Como é uma função, ela cria variáveis *scope*, então variáveis podem ser declaradas sem afetar o código fera da IIFE.  Exemplo: 
```js
(function IIFE(){
    console.log( "Hello!" );
})();
// "Hello!"
```

#### Clausura
Forma de *lembrar* e continuar acessando o escopo de uma função (e suas variáveis) mesmo se a função já estiver terminado de rodar.
Clausuras permitem você guardar estado — de tal forma, elas podem ser frequentemente utilizadas no lugar de objetos.

#### Módulos
A forma de uso mais comum de um clausura (closure) em JavaScript é o padrão módulo (module pattern).



#### Identificador `this`
Se em uma função há uma referência ao `this`, geralmente esse `this` aponta para um objeto e não se refere a função propriamente dita.