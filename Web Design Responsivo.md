# WEB DESING RESPONSIVO

## Autor: Tárcio Zemel

### Introdução: 
- **Web Desing Responsivo**: uma nova forma de pensar a web.
- **Técnicas**: layout fluído, imagens flexíveis, medias queries e etc.
- **One Web**: apenas uma URL para tudo, um sistema só e servir o mesmo conteúdo pra todo mundo (foco do livro).
- **RESS - Responsive desing + Server Side Components**: você serve a mesma URL, mesma página, mas ajusta no server-side algumas coisas sabendo qual browser é.


### Princípios de um web design responsivo:
- **3 tecnologias principais**: layout fluído (não especificação de medidas fixas no layout), imagens e recursos flexíveis e media queries.

**Resolução de Tela:**
- O que importa não é o tamanho físico do dispositivo e sim sua `resolução`.
- Com o uso da resolução de tela é possível desenvolver para uma maior quantidade de dispositivos.

**Layout Fluído:**
- Não usar medidas absolutas. Ao especificar, espaçamentos, margens, paddings, enfim, ao estipular qualquer medida referente ao layout das páginas do site, é preciso usar valores relativos (porcentagem, ems).
- Tipos de medida em CSS: `pixel` (um ponto indivisível na tela de exibição de um dispositivo), `point` (1/72 polegadas), `ems` (unidade escalável), `porcentagem`. Ems e porcentagem são relativos, escaláveis e se adaptam e mantêm relações de tamanho com outros elementos de um documento (possuem um contexto).
- `Porcentagem` para lidar com tamanho de layout e `Ems` para lidar com fontes.
- **Conversão de valor absoluto para relativo:** *Alvo* / *Contexto* = *Resultado*. - [Exemplo Prático](#).
    - Alvo: Elemento-alvo com a medida atual;
    - Contexto: Onde o elemento-alvo está (baseado no elemento-pai);
    - Resultado: o valor relativo que se está procurando.
    
### Exemplo Layout:
- [Código HTML](https://gist.github.com/3630605)
- [Código CSS](https://gist.github.com/3630828)
    
**Metatag Viewport:**
- Viewport: parte visível do página web que é renderizada pelos navegadores.
- Exemplo:
```html
<meta name="viewport" content="width=320,initial-scale=1">
```
    - width: define a largura da viewport;
    - heigth: define a altura da viewport;
    - initial-scale: define a escola inicial (zoom) inicial da *viewport*.
- Problema: para contemplar todos os dispositivos móveis, seria preciso conhecer a largura de cada um deles.
    - Solução: inidicar ao navegador que o `width` da *meta tag viewport* é o tamanho da largura do dispositivo.
    ```html
    <meta name="viewport" content="width=device-width,initial-scale=1">
    ```
    
**Alguns exemplos de conversão do layout fixo em fluído:**
- Tamanho do `contêiner`. Exemplo:
```html
.container {
    margin: 0 auto;
    width: 67.5% /* +/- 960 */
}
```
- Seria possível deixar responsivo para todos tipos de telas, colocando `width: 100%` no contêiner. Para projetos que precisam/queiram contar com largura total em quaisquer resoluções, seria o ideal.
- Tamanho do `h1`: 32 (alvo) dividido por 16 (contexto) é igual a 2 (resultado). Como para fontes usamos a medida em `em`:
```html
h1 {
    font-size: 2em; /* 32 / 16 */
}
```
- Tamanho do `.content`: 15 dividido por 960 (a medida de nossa já finada largura fixa) é igual a 0.015625 (para trabalhar com porcentagem multiplicamos esse valor por 100).
```html
.content {
    margin: 1.5625% 0; /* 15 / 960 */
}
```
- Tamanho do `.content-main`: não possui declaração explícita de largura, é preciso verificar o próximo elemento-ascendente (`.container`). Então nesse contexto, os 960 serão:
```html
.content-main {
    float: left;
    width: 61.7708%; /* 593 (.content-main) / (.container) */
}
```

### Imagens e recursos flexíveis:
**CSS para imagens flexíveis:**
- `max-width`: permite restringir larguras de conte 
údo dentro de um determinado intervalo. No caso abaixo significaria que as imagens poderiam ter no máximo 100% de largura do elemento em que estão contidas.
```html
img {
    max-width: 100%;
}
```

**CSS para outros recursos flexíveis:**
- A mesma regra aplicada para as imagens, podem ser aplicadas para outros tipos de mídia e recursos, incluindo `iframe, object, embed` e `video`.
```html
img, 
iframe, 
object, 
embed, 
video {
    height: auto;
    max-width: 100%;
}
```

**O problema de iagens em layouts fluídos:**
- Telas menores, muitas vezes resoluções não muito boas e velocidade de conexão inferior.
- No caso de dispositivos mobile, é melhor que seja usada uma versão reduzida da imagem, de menor peso e tamanho.

** Imagens de Alta Resolução:** seguir essas dicas trará benefícios em projetos que utilizam imagens em alta resolução.
- Não fazer requisição da mesma imagem várias vezes.
- Não usar cookie nem o elemento `<base>`.
- Manipulação mínima do DOM.
- Imagens devem continuar visíveis sem JavaScript.
- Não apresentar imagens em alta resolução para todos.

**Tipos de Imagem para Web:**
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
**Parâmetros para trabalhar com Media Queries**
- **aspect-radio**: descreve a proporção da aŕea de exibição do browser usado.
    ```html 
    @media screen and (aspect-ratio: 16/9) { }
    ```
    
- **color**: indica o número de birs por componente ede cor do dispositivo.
    ```html 
    @media all and (color) { }
    ```

- **color index**: descreve o número de entradas na tabela de cores do dispositivo.
    ```html
    @media all and (color-index) { }
    ```
    
- **device-aspect-radio**: descreve a proporção do *display* do dispositivo.
    ```html
    @media screen and (device-aspect-ratio: 16/9), screen and (device-aspect-ratio: 16/10) { }
    ```
    
- **device-height**: descreve a altura (pixels) do *display* do aparelho.
    ```html
    @media screen and (max-device-height: 379px) { }
    ```
- **device-width**: descreve a largura (pixels) do *display* do aparelho.
    ```html
    @media screen and (max-device-width: 799px) { }
    ```
- **grid**: determina se refere a um dispositivo de grade ou um dispositivo de mapa de bits (bitmap).
    ```html
    @media handheld and (grid) and (max-wdth: 15em) { }
    ```
- **height**: altura (pixels) da janela do navegador sendo usado.
    ```html
    @media screen and @media height: 300px) { }
    ```