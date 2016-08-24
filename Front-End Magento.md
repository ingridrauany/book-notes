# Curso: Front-End Magento

## Autor: Ricardo Martins

### Estrutra de Pastas

Contém todos os arquivos php do Magento, pasta da aplicação. Dentro dela temos:

- `app`: 
    - `/code`: contém os módulos.
        - `/community`: módulos da comunidade.
        - `/core`: módulos do núcleo do magento,  onde é recomendado que nunca se altere diretamente.
        -  `/local`: módulos locais que contém alterações ou módulos especificos da loja usada.
- `/design`:
    - `/adminhtml`: onde estão arquivos de template e design da parte administrativa (back-end da loja).
    - `/frontend`: estilos e arquivos de template/xml/phtml que irão afetar o front-end da loja.
    - `/install`: relacionado ao instalador do magento.
- `/etc`: contém arquivos de configuração do magento.
    - Um dos principais arquivos é o `local.xml`  que contém informação da base de dados.
    - `/modules`: contém os xmls dos módulos, onde é possível habilitar ou desabilitar módulos da loja.
- `/locale`: contém as traduções do magento.
- `/js`: contém todos os arquivos javascript do core do magento.
- `/media`: contém todas imagens da loja (ex: catálogo ou módulos de terceiros).
- `/shell`: arquivos acessados pelo terminal.
- `/skin`: especifícos do tema ou pacotes de tema.
- `/var`: contém arquivos temporários (ex: cache, sessão e log).

### Hierarquia de Temas

Pacote que contém um ou mais temas, o magento procura nos arquivos xml como ele deve montar as páginas da loja, que ficam alocados nessas pastas:
- `app/design/frontend/`
- `skin/frontend`

Se nada for configurado no Magento, ele sempre vai procurar o tema default no pacote.

### Alteração de temas

Uma das formas de alterar o tema é através da página administrador da loja, em `configurações -> visual ou design`.

Outra forma é criar o próprio tema e fazer alterações necessárias.

Datas comemorativas: alterar temas e especificar o período onde a loja será afetada por determinado tema.

#### Fallback de temas

Exemplo: o tema da categoria sobrepõe a configuração de tema global.

### Pacotes e Temas

Para criar um tema é necessário criar as pastas pacote e do tema em:
- `app/design/frontend/`
- `skin/frontend`

A maior parte do tema é herdado do `/base`. É possível herdar o conceito de um outro tema e modificar apenas o necessário dentro do nosso tema.

### XMLs de Layout

- Alterar, remover, mover e criar blocos nos temas.
- Age diretamente sobre blocos e classses.
- Chamar métodos php nos blocos.

Os arquivos de xml ficam em: `app/design/frontend/[pacote]/[tema]/layout/*.xml`. Os módos do magento possuem seu próprio arquivo de layout, ex: `Mage_Customer -> customer.xml`

Os arquivos XML são divididos em **handles** (nós), o magento já possui alguns pré-definidos. Ex: cliente logado/não logado, listagem de produtos de categorias. 

### Blocos e processamento XML

Tipos de blocos: estruturais e conteúdo. Magento faz um merge (juntar) das alterações que cada xml faz nos handles da loja.


**Blocos Estruturais**: definem estrutura visual da loja (ex: header, footer, content).

**Blocos de Conteúdo**: produzem conteúdos que ficam alocados dentro de blocos estruturais.

### Estrutura do XML

Magento renderiza todos os handles e tudo o que está abaixo deles.
- Handles: sevem para o magento saber quando deve renderizar alguma coisa. O handles `default` é carregado em quase toda as páginas.
- Blocks: 
	- `type`: qual classe php que representa o bloco.
	- `name`: único.
	- `before` e `after`: utilizando apenas quando o bloco está dentro de um bloco estrutural.
	- `template`: indica ao magento qual arquivo phtml que vai representar o template.
	- `as`: utilizado em blocos do tipo estrutural, tem prioridade sobre o `name`.
	- Action: chama um método dentro da classe php.
- References: referencia para o magento sobre qual bloco você quer trabalhar.

### Inserindo JS e CSS em páginas específicas

O método `addJs` insere os arquivos a partir da pasta js do core do magento.

Os métodos `addCss` e `addItem` procura os arquivos no tema que está sendo renderizado.

### Bloco com arquivo de template

Exemplo:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<layout>
    <default>
        <reference name="content">
            <block name="inteligente" type="core/template" template="home/teste.phtml"></block>    
        </reference>
    </default>
</layout>
```

### Blocos Estáticos

Blocos que não sofrem alterações o próprio cliente pode controlar pelo painel da loja. O conteúdo pode ser somento texto ou tags html.

Exemplo (bloco de telefone da loja no rodapé):

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<layout>
    <default>
        <reference name="footer">
            <block name="telefone.rodape" type="cms/block">
                <action method="setBlockId"><param>telefone</param></action>
            </block>    
        </reference>
    </default>
</layout>
```

- `cms/block`: representa a classe de blocos estáticos do CMS do magento.

- `param`: parâmetro do bloco chamado.

### Validação de formulários com JavaScript

Todas as validações de campo funcionam atráves de classes css. Ex: `class = required-entry`.

Arquivo: `js/prototype/validation.js` = todas as classes de validação do magento.

### Estendendo uma classe JavaScript nativa

Exemplo:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<layout>
    <PRODUCT_TYPE_configurable>
        <reference name="head">
            <js>configuravel.js</js>   
        </reference>
    </PRODUCT_TYPE_configurable>
</layout>
```

Na pasta `js` você cria o arquivo para utilizar o método do prototype (wrap) para sobrescrever o método original.

### Estrutra e desenvolvimento

- Criação do pacote e tema.
- `getChildHtml`: chama um bloco estrutural.
- Updates de layout: atualização dos comportamentos padrões.
Exemplo:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<layout>
    <catalog_category_view>
        <reference name="root">
            <action method="setTemplate">
                <template>page/2columns-left.phtml</template>
            </action>
        </reference>
    </catalog_category_view>
</layout>
```