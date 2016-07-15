# WEB DESING RESPONSIVO

## Autor: Tárcio Zemel

### Introdução: 
- **Web Desing Responsivo**: uma nova forma de pensar a web.
- **Técnicas**: layout fluído, imagens flexíveis, medias queries e etc.
- **One Web**: apenas uma URL para tudo, um sistema só e servir o mesmo conteúdo pra todo mundo (foco do livro).
- **RESS - Responsive desing + Server Side Components**: você serve a mesma URL, mesma página, mas ajusta no server-side algumas coisas sabendo qual browser é.


### Princípios de um web design responsivo:
- **3 tecnologias principais**: layout fluído (não especificação de medidas fixas no layout), imagens e recursos flexíveis e media queries.

#### Resolução de Tela:
- O que importa não é o tamanho físico do dispositivo e sim sua `resolução`.
- Com o uso da resolução de tela é possível desenvolver para uma maior quantidade de dispositivos.

#### Layout Fluído:
- Não usar medidas absolutas. Ao especificar, espaçamentos, margens, paddings, enfim, ao estipular qualquer medida referente ao layout das páginas do site, é preciso usar valores relativos (porcentagem, ems).
- Tipos de medida em CSS: `pixel` (um ponto indivisível na tela de exibição de um dispositivo), `point` (1/72 polegadas), `ems` (unidade escalável), `porcentagem`. Ems e porcentagem são relativos, escaláveis e se adaptam e mantêm relações de tamanho com outros elementos de um documento (possuem um contexto).
- `Porcentagem` para lidar com tamanho de layout e `Ems` para lidar com fontes.
- **Conversão de valor absoluto para relativo:** *Alvo* / *Contexto* = *Resultado*.
    - Alvo: Elemento-alvo com a medida atual;
    - Contexto: Onde o elemento-alvo está (baseado no elemento-pai);
    - Resultado: o valor relativo que se está procurando.
    
### Exemplo Layout:
- [Código HTML](https://gist.github.com/3630605)
- [Código CSS](https://gist.github.com/3630828)
    
#### Metatag Viewport:
- Viewport: parte visível do página web que é renderizada pelos navegadores.
- Exemplo:
```html
<meta name="viewport" content="width=320,initial-scale=1">
```

**width**: define a largura da viewport;
    
**heigth**: define a altura da viewport;
    
**initial-scale**: define a escola inicial (zoom) inicial da *viewport*.

- Problema: para contemplar todos os dispositivos móveis, seria preciso conhecer a largura de cada um deles.

    - Solução: inidicar ao navegador que o `width` da *meta tag viewport* é o tamanho da largura do dispositivo.
    ```html
    <meta name="viewport" content="width=device-width,initial-scale=1">
    ```
    
#### Alguns exemplos de conversão do layout fixo em fluído:
- Tamanho do `contêiner`. Exemplo:
```css
.container {
    margin: 0 auto;
    width: 67.5% /* +/- 960 */
}
```

- Seria possível deixar responsivo para todos tipos de telas, colocando `width: 100%` no contêiner. Para projetos que precisam/queiram contar com largura total em quaisquer resoluções, seria o ideal.
- Tamanho do `h1`: 32 (alvo) dividido por 16 (contexto) é igual a 2 (resultado). Como para fontes usamos a medida em `em`:
```css
h1 {
    font-size: 2em; /* 32 / 16 */
}
```

- Tamanho do `.content`: 15 dividido por 960 (a medida de nossa já finada largura fixa) é igual a 0.015625 (para trabalhar com porcentagem multiplicamos esse valor por 100).
```css
.content {
    margin: 1.5625% 0; /* 15 / 960 */
}
```

- Tamanho do `.content-main`: não possui declaração explícita de largura, é preciso verificar o próximo elemento-ascendente (`.container`). Então nesse contexto, os 960 serão:
```css
.content-main {
    float: left;
    width: 61.7708%; /* 593 (.content-main) / (.container) */
}
```

### Imagens e recursos flexíveis:
#### CSS para imagens flexíveis:
- `max-width`: permite restringir larguras de conte 
údo dentro de um determinado intervalo. No caso abaixo significaria que as imagens poderiam ter no máximo 100% de largura do elemento em que estão contidas.
```css
img {
    max-width: 100%;
}
```

#### CSS para outros recursos flexíveis:
- A mesma regra aplicada para as imagens, podem ser aplicadas para outros tipos de mídia e recursos, incluindo `iframe, object, embed` e `video`.
```css
img, 
iframe, 
object, 
embed, 
video {
    height: auto;
    max-width: 100%;
}
```

#### O problema de iagens em layouts fluídos:
- Telas menores, muitas vezes resoluções não muito boas e velocidade de conexão inferior.
- No caso de dispositivos mobile, é melhor que seja usada uma versão reduzida da imagem, de menor peso e tamanho.


#### Imagens de Alta Resolução: 
Seguir essas dicas trará benefícios em projetos que utilizam imagens em alta resolução.
- Não fazer requisição da mesma imagem várias vezes.
- Não usar cookie nem o elemento `<base>`.
- Manipulação mínima do DOM.
- Imagens devem continuar visíveis sem JavaScript.
- Não apresentar imagens em alta resolução para todos.

#### Tipos de Imagem para Web:
- **GIF:** formato sem perda, suporta "transparência binária".
- **JPG (ou JPEG):** formato 24 bits (boa qualidade), boa taxa de compressão, formato com perda, não aceita transparência.
- **PNG:** pode ser PNG 8 bits ou PNG 24 bits, formato sem perda, provendo suporte a 256 cores e transparência binária.
- **SVG:** podem ser usadas em qualquer lugar, escola e resolução, formato vetorial (pode ser redimensionado).
- **Icons fonts:** gráficos que na verdade são fontes, pode aumentar ou diminiuir sem a perda de resolução.

### Media Queries

É necessário que os elementos do site além de flexíveis, possam variar de posição, tamanho, se escondam ou apareçam, conforme a necessidade.

- Recomendação da W3C desde o CSS2.
- Tipos de **media**: all, braile, embossed, handheld, print, projection, screen, speech, tty e tv.

Exemplo: podemos indicar um CSS somente para devices com tela de até 320px
```html
<link rel="stylesheet" media="screen and (max-width: 320px)" href="320.css">
```
##### Parâmetros para trabalhar com Media Queries

- **aspect-radio**: descreve a proporção da aŕea de exibição do browser usado.
```css
@media screen and (aspect-ratio: 16/9) { }
```
    
- **color**: indica o número de birs por componente ede cor do dispositivo.
```css 
@media all and (color) { }
```

- **color index**: descreve o número de entradas na tabela de cores do dispositivo.
```css
@media all and (color-index) { }
```
    
- **device-aspect-radio**: descreve a proporção do *display* do dispositivo.
```css
@media screen and (device-aspect-ratio: 16/9), screen and (device-aspect-ratio: 16/10) { }
```
    
- **device-height**: descreve a altura (pixels) do *display* do aparelho.
```css
@media screen and (max-device-height: 379px) { }
```
    
- **device-width**: descreve a largura (pixels) do *display* do aparelho.
```css
@media screen and (max-device-width: 799px) { }
```

- **grid**: determina se refere a um dispositivo de grade ou um dispositivo de mapa de bits (bitmap).
```css
@media handheld and (grid) and (max-wdth: 15em) { }
```

- **height**: altura (pixels) da janela do navegador sendo usado.
```css
@media screen and @media (height: 300px) { }
```

- **monochrome:** indica o número de bits por pixel em dispositivos monocromáticos.

- **orientation:** indica se o dispositivo está em modo *paisagem* ou *retrato*.
```css
@media all and (orientation: landscape) { }
```

- **resolution**: resolução do dispositivo (densidade de pixels).

- **scan:** tipo de processo de escaneamento que o dispositivo do tipo "TV" pode fazer.

- **width:** largura (pixels) da tela do navegador.
```css
@media screen and @media (max-width: 767px) { }
```

#### Operadores Lógicos

- **and e or:** a palavra *and* expressa o operador lógico **and** e a *vírgula* o operador lógico **or**.
- **not:** a presença *not* no início da consulta nega o resultado.
- **only:** 

#### Gerenciamento de erros
- Tipos de mídia desconhecidos serão avaliados como *false*.
- Agentes de usuário interpretam como *not all* quando um dos **valores** de um paramêtro for desconhecido.
- Agentes de usuário conseguem lidar com símbolos inesperados encontrados ao analisar uma consulta de mídia (erro de sintaxe).

#### Uso Consciente de Media Queries
- É recomendado que seja utilizado somente uma folha de estilos (apenas uma requisição HTTP).
- *Empilhar* breakpoints: quando estilos entre eles são bem diferentes. *Sobrepor* breakpoints: quando não há muitas diferenças.
- Uso de soluções JavaScript para problema de não-suporte no IE8 (se o uso desse navegador pelo seu público for alto).

### Web Mobile

#### Mobile First
Primeiro planeja o design para dispositivos *móveis* progredindo até ao *desktop*.
- Permite atingir todos os *devices*.
- Otimizar a experiência para o novo contexto sem ter que recriá-lá.
- Foco no que é importante e essencial dentre as funcionalidades do projeto.

#### Uso dos dispositivos móveis
Saber como o seu público utiliza os dispositivos móveis para gerar uma melhor experiência para o usuário.
- Perfis de uso: *pesquisar* (urgente, local), *explorar/divertir* (entendiado, local), *check in/status* (repetição, micro-tarefas), *editar/criar* (mudança urgente, micro-tarefas).
- Horário e local de uso.

#### Conteúdo
Quando se trata de dispositivos móveis não há espaço para elementos que não agregem à experiência de uso. É necessário dar atenção as tarefas mais comuns dos usuários.

#### Padrões de Navegação Mobile
- Top Nav: navegação no topo (fácil implementação, porém não é escalável).
- Âncora no rodapé: lista de navegação no rodapé do site e no topo existe um link apontando para a navegação no rodapé (pode confundir alguns usuários).
- Menu de seleção: lista de links em um menu de seleção para telas menores (ocupa menos espaço, mas pode parecer confuso). 
- Alternância: link para que o menu se abra no próprio local (facilmente escalável).
- Slide à esquerda: ícone de menu que exibe o menu através de uma animação de slide que começa á esquerda (não ocupa espaço em tela).
- Navegação Pull Down: slide que mostra o menu e empurra o restante do conteúdo para baixo.

#### 10 Princípios de design para interfaces mobile

1 - Mentalidade móvel: imersão na mentalidade *mobile*.

2 - Contexto móvel: entendiado (sessão de maior tempo de uso, mas com possilidades de interrupção), ocupado (micro-tarefas de forma rápida e confiável) e perdido (conectividade e bateria).

3 - Orientações gerais: responsividade, polidez , dedos (polegares são o padrão), alvos (padrão de elementos: 44 pixels), conteúdo (em foco), controles (parte inferior), rolagem (evitar).

4 - Modelos de navegação: escolher o que faz mais sentido para a aplicação.

5 - Inputs do usuário: facilitar a digitação (ex: type do input vai determinar teclado)

6 - Gestos: invisibilidade (revelar existência do gesto para o usuário), duas mãos (possibilitar a navegação com apenas uma mão disponível), bom de ter (apenas usuários avançados identificam) e sem substituição (ainda não há padrão geral de gestos, certos controles devem ser visíveis).

7 - Orientação: *portrait* mais popular.

8 - Comunicações: feedback imediato, evitar alertas modais e pedir confições de ações.

9 - Inicialização do aplicativo: tela desprovida de conteúdo com apenas a logo ou uma imagem.

10 - Primeiras Impressões: ícone (mostrar ideia do que o app faz), primeiro lançamento (facilidade para o usuário se familiarizar com o app).