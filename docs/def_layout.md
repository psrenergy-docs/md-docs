---
title: Definição de layout
nav_order: 2
---

# Definição de layout
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

Os arquivos XML são utilizados para configuração da interface do MDStudio. A parte inicial dos nomes dos arquivos (representado por asterisco) pode ser alterada, porém a parte final do nome do arquivo deve manter o padrão listado abaixo. Estes arquivos XML são divididos em:

* CollectionLayout.xml: Onde é definido quais atributos serão mostrados, quais são editáveis e de que forma são agrupados. 
  
* TreeView.xml: Onde é configurado a árvore de coleções para navegação do usuário.
  
* LayoutDictionary.xml: Onde será configurado as traduções customizadas da interface, como grupos, navegação, nome customizável de tabela etc.
  
* ExecutionTemplate.xml: Onde será configurado todos as execuções, scripts ou chamadas de outras aplicações da interface.

* ToolsTemplate.xml: Onde será configurado os botões e grupos para as execuções na interface.
  
* LoadTemplate.xml: Único por aplicação onde define quais tipos de dados serão carregados.

## Layout inicial do caso

Os arquivos relacionados com a construção da visualização inicial do caso no MDStudio são os arquivos XML:

1.	Treeview.xml
2.	CollectionLayout.xml

O arquivo TreeView.xml possui tags para realizar as separações necessárias para a divisão dos itens no formato de árvore e está localizado no lado esquerdo da interface (em laranja). Enquanto o arquivo *CollectionLayout.xml possui as informações para montar as seções do lado direito (em verde) referente a cada um desses itens (Figura 3).  

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig3_v1.png" width="600"/>
</div>

### TreeView.xml

No arquivo *TreeView.xml é possível iniciar a construção da árvore utilizando a tag TemplateGroup, sendo apenas necessário apenas o preenchimento do atributo Name, geralmente se referindo ao nome do modelo utilizado. Para criar um item para esta árvore, é preciso adicionar a tag TemplateCollection, preenchendo os atributos como Name de acordo com os nomes das classes no arquivo pmd. Para alterar o nome que será mostrado, basta alterar o nome da coleção no arquivo *LayoutDictionary.xml. As instruções para esta alteração estão presentes na seção XXX.

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig4_v1.png" width="600"/>
</div>

### CollectionLayout.xml

No arquivo *CollectionLayout.xml, encontra-se outras divisões do layout, separadas em tags.
A tag **ElementCollection** é a primeira a ser definida. Ela se refere a cada coleção (ou classe), onde é possível também definir todas as suas características. Esta tag aparece na interface como visto na figura 3, equivalente ao mostrado como o *CollectionLayout.xml. Um exemplo do arquivo xml do uso do ElementCollection encontra-se na Figure 5. Esta tag pode conter várias flags, os essenciais são:

* **Name**: Representa o nome da coleção definida no PSRClasses ou a que foi definida no arquivo pmd;
  
* **Model**: Representa o modelo que será utilizado como base para a coleção;

Os parâmetros definidos no arquivo pmd serão definidos neste arquivo xml como **atributos** (Attribute). Os parâmetros atributos identificados com @id no arquivo pmd, são caracterizados como atributos identificadores, sendo definidos dentro da tag **InfoAttributes**. Todas as coleções precisam ter atributos identificadores.

Dentro da tag ElementCollection é possível criar outras tags para definir como os atributos serão apresentados na interface. São divididas em (Figura 5):

I.	**GroupCollection**: Onde é possível definir grupos para dividir os atributos em abas (em amarelo).

II.	**NavigationCollection**: Onde será definido a estrutura de navegação das tabelas e grupos (em roxo);

III.	**Attributes**: Onde serão definidos os parâmetros da coleção que foram previamente definidos no pmd (em vermelho);

IV.	**TableAttributes**: onde serão definidos os vetores e tabelas da coleção que foram previamente definidos no pmd (em azul);

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig6_v1.png" width="600"/>
</div>

I.	**GroupCollection**

O grupo usa a tag “<Group></Group>”, podendo definir quantos grupos quiser, respeitando códigos distintos (na mesma coleção). Com a principal função para dividir os atributos em diversos contextos por tipo de elemento. Os atributos que podem ser definidos na tag são:

*	**Code**: Representa a identificação única do grupo e usado para associar ao atributo;

*	**IsHidden**: Representa se o grupo inicializará escondido, caso seja igual a “True” ficará escondido, valor default é “False”;

*	**Translation**: Representa o nome da tradução desejada definida no xml de traduções (*LayoutDictionary.xml);

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig7_v1.png" width="600"/>
</div>

II.	**NavigationCollection**:

A navegação vai organizar a visualização dos grupos, tabelas e dados cronológicos. A tag “<Navigation></Navigation>” usada para definir uma navegação. Exemplo da utilização do NavigationCollection é mostrado na Figure 8.

*	**Name**: Nome único de identificação para a navegação (por coleção).

*	**Items**: Definição de quais itens vão ser atrelados a esta navegação. Um item de navegação pode ser um grupo de atributos ou um atributo tabela, pode colocar N itens atrelados ao nó “<Navigation>”. A tag usada no item é “<NavigationItem></ NavigationItem>”.
    * **Name**: Representa o Código do grupo desejado ou o nome do atributo tabela definido .
  
**Obs**: Todas as tabelas caso não tenha dados seu nome fica em cinza claro.

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig8_v1.png" width="600"/>
</div>

III.	**Attributes**

Os atributos padrões definidos no pmd (como PARM) serão definidos nesta tag. Cada um deles será mostrado na interface como uma coluna em seu determinado grupo e como um campo na tela de “Properties”. Mais informações sobre atributo serão dadas na seção XXX.  Exemplo da utilização do Attributes é mostrado na Figure 9.

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig9_v1.png" width="600"/>
</div>

Se definido um grupo é possível utilizar a flag Group, para fazer referência ao grupo em que o atributo faz parte. 

IV.	**TableAttributes**

O modo de visualização de um parâmetro vetor é dado em forma de tabela. Existem alguns padrões como modificação (registros espaçados), dados em blocos de anos fechados (cronológicos), modificações com cadastro (data de 1900), etc. Os parâmetros do tipo dimensão também são visualizados através de uma tabela. O tipo de visualização das tabelas é dado pelo campo “IndexType”, dependendo do número, o atributo é montado na tela de forma diferente (respeitando o tipo do dado). Todos os atributos do tipo tabela devem ser definidos na tag <TableAttributes>. Mais informações sobre atributo serão dadas na seção XXX. Exemplo da utilização do TableAttributes é mostrado na Figure 10.

<div style="text-align:center">
    <img src="images\ModelagemDados\DocOrigFig10_v1.png" width="600"/>
</div>
