# You Don't Know JS - Scope & Closures

## Autor: Kyle Simpson
### Tradução: [Cezar Augusto](https://github.com/cezaraugusto/You-Dont-Know-JS)

## Capítulo 1 - O que é um Escopo
*Estado* de um programa: habilidade de armazenar e pegar valores de variáveis.

*Escopo*: regras para armazenar variáveis em algum lugar e encontrá-las depois.

### Teoria de Compiladores
JavaScript é uma linguagem compilada, porém com não muita antecedência.

Processo tradicional de uma linguagem compilada: 

1 - **Tokenização:** quebra string de caracteres de modo que façam sentido para a linguagem = tokens.

Exemplo: `var a = 2;` seria quebrado em: `var`, `a`, `=`, `2` e `;`.

2 - **Análise:** transformar conjunto de tokens em uma árvore de elementos alinhados (AST).

3 - **Geração de Código:** obter a AST e transformar em código executável. 

Para Javascript a compilação acontece pouco antes do código ser executado. O compilador JS obtém o programa `var a = 2;` e compila ele antes e de imediato está pronto para executá-lo.

### Entendendo o Escopo

#### Elementos

1 - *Motor:* responsável pela compilação e execução do programa javascript.

2 - *Compilador:* análise e geração de código.

3 - *Escopo:* contém lista de consultas a todos os identificadores declarados (variáveis) e impõe regras de como esses identificadores ficam visíveis para o código em execução.

#### Funcionamento
O *motor* vê duas instruções distintas, uma que o *compilador* gerencia e outro que o próprio *motor* gerencia. Então, o modo que o programa `var a = 2;` é abordado é:

- Análise lexíca, quebra o programa em tokens que serão transformados em uma árvore AST;
- O *compilador* encontra a `var a` e pede para ver se existe algum `a` para o conjunto particular desse *escopo*. Se não houver, então o *compilador* pede ao *escopo* para declarar uma variável chamada `a`.
- Então o *compilador* produz o código (que gera atribuição `a = 2`) para o *motor* (código que o *motor* executa pergunta se existe a variável `a`).

**Resumo:** *compilador* declara uma variável e quando executar, o *motor* busca a variável no *escopo* e atribui a ela o valor.

#### Compilador

O tipo de busca pela variável (`a`) que o *motor* faz pode ser **LHS** (left-hand side) ou **RHS** (right-hand side), o "lado" se refere ao lado **da operação de atribuição**.

- LHS: quando a variável aparece do lado esquerdo da operação de atribuição (alvo da atribuição). Ocorrem com o uso do operador `=` ou passagem de argumentos para uma função. Exemplo:
    ```js
    a = 2;
    ```
- RHS: quando a variável não aparece do lado esquerdo de uma atribuição (fonte da atribuição). Exemplo:

    ```js
    console.log( a );
    ```
    
### Escopos Aninhados

Percurso dos *Escopos Aninhados*: o *motor* inicia no *escopo* que está em execução, caso precise sobe de nível e assim por diante (ao chegar no escopo global, se a variável não for achada a busca é encerrada).

### Erros

`ReferenceError`: está relacionado à falha na resolução do *escopo*.

`TypeError`: sugere que a resolução de *escopo* foi bem sucedida, mas houve uma tentativa de operação ilegal/impossível no resultado que foi obtido.

## Capítulo 2 - Escopo Léxico

### Hora do Léxico

Escopo léxico é o *escopo* definido durante a etapa de análise léxica. 

```js
function foo(a) {

    var b = a * 2;

    function bar(c) {
        console.log( a, b, c );
    }

    bar(b * 3);
}

foo( 2 ); // 2 4 12
```

- Escopo global: possui apenas o identificador `foo`.
- Escopo de `foo`: possui 3 identificadores: `a`, `bar` e `b`.
- Escopo de `bar`: possui apenas o identicador `c`.

#### Consultas

A estrutura e relação de posicionamento dos escopos descreve para o *motor* os locais onde deve consultar para localizar um identificador.

- A consulta de escopo termina assim que uma ocorrência é localizada.
- *Shadowind* (sombreamento): definir um mesmo identificador em diferentes camadas de escopo aninhadas.
- Consulta de escopo sempre se inicia no escopo mais próximo do ponto de execução atual e segue de fora/cima até a localização de uma ocorrência.
- O escopo léxico de uma função é definido *apenas* pelo local onde a função foi declarada.

### Trapaceando o Léxico

Má prática que leva a um pior desempenho. Modifica o escopo léxico após a fase de *tokenizing*.

#### `eval`

Essa função recebe uma string como argumento e trata o conteúdo da string como se tivesse de fato sido programado pelo autor do código naquele ponto do programa. A *Engine* não vai saber se aquele código JavaScript que foi passado como paramêtro foi gerado pelo compilador ou injetado. Exemplo:

```js
function foo(str, a) {
    eval(str);
    console.log(a, b);
}
 
var b = 2;
foo("var b = 3;", 1);
```

#### `with`

"Atalho" para a criação de diversas referências à propriedades de um determinado objeto sem precisarmos referenciá-lo em cada uma delas. A instrução `with` cria um escopo léxico totalmente novo a partir do objeto passado. Exemplo:

```js
function foo(obj) {
    with (obj) {
        a = 2;
    }
}

var o1 = {
    a: 3
};

var o2 = {
    b: 3
};

foo( o1 );
console.log( o1.a ); // 2

foo( o2 );
console.log( o2.a ); // undefined
console.log( a ); // 2 -- Opa, "vazou" para o escopo global!
```

Quando `o2` é utilizado como "escopo" e não possui identificador `a`. O identificador `a` não é achado no escopos de `o2`, `foo(...)` e global, isso resulta na criação da variável global.


#### Performance

Funções como `eval` e `with` faz com que otimizações não sejam executadas.

## Capítulo 3: Escopo de Função vs Bloco de Escopo

Escopo: "bolhas" nas quais os identificadores são declarados.

### Escopo a partir de Funções

Cada função declarada cria uma "bollha" para si. As variáveis pertencem à função e podem ser reutilizadas pela sua extensão e não vão estar acessível fora do seu escopo.

### Escondendo-se em pleno escopo
Variáveis e funções podem ser escondidas ao serem envolvidas por um escopo de uma função.

- Princípio do privilégio mínimo. Exemplo: 

```js
function doSomething(a) {
    b = a + doSomethingElse( a * 2 );

    console.log( b * 3 );
}

function doSomethingElse(a) {
    return a - 1;
}

var b;

doSomething( 2 ); // 15
```

Dar "acesso" a `b` e `doSomethingElse(...)` ao escopo superior é desnecessário e "perigoso". De forma mais adequada: 

```js
function doSomething(a) {
    function doSomethingElse(a) {
        return a - 1;
    }

    var b;

    b = a + doSomethingElse( a * 2 );

    console.log( (b * 3) );
}

doSomething( 2 ); // 15
``` 

Agora `doSomething(...)` controla `b` e `doSomethingElse(...)`.

### Collision Avoidance
Evitar colisão de dois identificadores diferentes com mesmo nome, porém com diferentes usos.

### Global "Namespaces"
Bibliotecas carregadas no programa podem colidir entre elas se não esconderem de forma adequada suas funções privadas e variáveis.