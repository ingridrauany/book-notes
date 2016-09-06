# Eloquent JavaScript

## Autor: Kyle Simpson
### Tradução: [Eric Douglas](https://github.com/braziljs/eloquente-javascript)

## 1 - Valores, Tipos e Operadores

### Valores

**Tipos:** números, strings, booleanos, objetos, funções e valores indefinidos.

#### Números

JavaScript utiliza um número fixo de bits (64) para armazenar um valor númerico. Cálculo com números fracionários não são precisos.

#### Números Especiais

São considerados números, mas não se comportam como números normais: `Infinity`, `-Infinity` e `NaN` (not a number -  recebemos como resultado quando tentamos calcular por exemplo: `0/0`, `Infinity-Infinity`).

#### Operadores Unários

Operadores escritos com palavras, exemplo: `typeof`.

```js
console.log(typeof 4.5)
// → number
```
#### Boolean

Existe apenas um valor no JavaScript que não é igual a ele mesmo: `NaN`.

```js
console.log(NaN == NaN)
// → false
```

#### Valores Indefinidos

Existem dois tipos: `null` e `undefined`. `null`: valor primitivo utilizado quando uma variável não teve valor atribuído, `undefined`: valor primitivo que representa a ausência intencional de um valor objeto.

#### Conversão Automática de Tipo

Quando um operador é aplicado a um tipo de valor "errado", o JavaScript converterá (*coerção de tipo*) esse valor para o tipo que ele desejar, seguindo regras.

#### O Curto-Circuito de  && e ||

O operador `||` retorna o valor à sua esquerda quando ele puder ser convertido em `true`, ao contrário ele retornará o valor à sua direita. Exemplo: 

```js
console.log(null || "user")
// → user

console.log("Karl" || "user")
// → Karl
```
O operador `&&` trabalha de forma contrária, retorna o valor à sua esquerda se ele puder ser convertido em `false`, caso contrário retorna o valor à sua direita.


## 2 - Estrutura do Programa

### Fluxo de Dados

As declarações são executadas de baixo para cima e o fluxo de controle em linha reta é feita da esquerda para a direita.

### Loops While e Do

A diferença entre eles, é que o `do` executa suas declarações ao menos uma vez e testa se deve para ou não após a primeira execução.

## 3 - Funções