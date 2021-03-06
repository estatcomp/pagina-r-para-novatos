---
title: "Gerenciamento de projetos com RStudio"
teaching: 20
exercises: 10
questions:
- "Como eu posso gerenciar meus projetos no R ?"
objectives:
- Ser capaz de criar projetos independentes com RStudio
- Usar o git com RStudio
keypoints:
- "Utilizar o RStudio para criar e gerenciar projetos com bom layout."
- "Tratar os dados apenas como arquivos de leitura."
- "Tratas as saídas como dispensáveis."
- "Separar as funções das aplicações."
- "Usar a versão de controle"
---




## Introdução

O processo científico é de natureza incremental. Muitos projetos começam com notas ou códigos aleatórios e a partir disso surgem manuscritos. Eventualmente essas escritas e códigos se misturam.
<blockquote class="twitter-tweet"><p>Managing your projects in a reproducible fashion doesn't just make your science reproducible, it makes your life easier.</p>— Vince Buffalo (@vsbuffalo) <a href="https://twitter.com/vsbuffalo/status/323638476153167872">April 15, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

A maioria das pessas organizam seus projetos da seguinte maneira

![](../fig/bad_layout.png)

Por diversas razões SEMPRE devemos evitar esse tipo de armazenamento de projetos:

1. É difícil ver qual versão é a original e quais são as modificadas.
2. Deste modo obtemos diversas extensões de arquivos na mesma pasta.
3. Provavelmente iremos demorar bastante para para encontrar alguma coisa. Relacionar uma figura com o código que a gera, por exemplo.

Um bom *layout* pode facilitar bastante nossa vida. Algumas vantagens são:

* Nos ajuda a assegurar a integridade dos dados;
* Facilita o compartilhamento dos códigos com outras pessoas (colegas de laboratório, colaboradores ou supervisores);
* Facilita o processo de atualização dos códigos;
* É mais fácil encontrar um projeto após algum tempo.

## Uma possível solução

Existem ferramentas e pacotes que nos ajudam a gerenciar nosso trabalho de forma mais efetiva.

Uma das melhores características do RStudio, são as funcionalidades oferecidas em termos de gerenciamento de projetos. Usaremos tais ferramentas para uma criar um projeto independente e passível de ser reproduzido.



> ## Desafio: Criando um projeto independente
>
> Vamos criar um novo projeto no RStudio
>
> 1. Clique no botão File e então em  New Progect.
> 2. Clique em New Directory.
> 3. Clique em Empty Project.
> 4. Digite o nome do diretório que em que seu projeto será gravado.
> 5. Clique em Create a git repository.
> 6. Clique em Create Projeto.
{: .challenge}

Agora, toda vez que iniciarmos uma sessão desse projeto no RStudio todo o trabalho estará inteiramente contido neste diretório.

## Melhores práticas aplicadas a organização de projetos

Embora não exista a `MELHOR` forma de organizar um projeto, existem alguns princípios gerais que são consistentes com o objetico de deixar o gerenciamento de projetos mais simples.

### Trate os dados apenas como leitura

Este é provavelmente o principal objetivo ao organizar um projeto. Dados geralmente são difíceis de se coletar. Trabalhar com dados em programas interativos (Excel) onde eles podem ser modificados atrapalha. Isso porque não temos certeza de onde os dados vieram ou como foram modificados desde a coleta. Para evitar este tipo de problema é recomendável trabalhar os dados como arquivos apenas para leitura.

### Limpeza dos dados

Em muitos casos os dados são "sujos". Nestes casos é extremamente difícil transformar os dados até que eles sejam passíveis de serem lidos pelo R (ou qualquer outro programa). Esta tarefa é geralmente chamada de "data munging". Quando alterações devem ser feitas no conjunto de dados original, é aconselhável criar um segundo arquivo de leitura em uma pasta separada.

### Trate as saídas como dispensáveis

Quaisquer coisas geradas pelos scripts devem ser tratadas como dispensáveis. Devemos ser capazes de recriar as alterações ou análises feitas a partir do script.

Existem diversas maneiras de gerenciar os outputs. É interessante termos uma pasta com subdiretórios para cada análise que formos fazer. Desta maneira é mais fácil encontrar as análises de interesse, pois ao mesmo tempo que nem todas as análises feitas são utilizadas no trabalho final, outras poderão ser aplicadas em outros projetos.


> ## Dica: Praticas interessantes em computação científica
>
> [Boas práticas em computação científica](https://github.com/swcarpentry/good-enough-practices-in-scientific-computing/blob/gh-pages/good-enough-practices-for-scientific-computing.pdf) sugerem as recomendações para uma boa organização de projetos:
>
> 1. Coloque cada projeto em seu próprio diretório. O diretório deve ser nomeado após o projeto.
> 2. Coloque documentos de textos associados a um diretório `doc`.
> 3. Coloque os dados puros no diretório `data`, os dados alterados e os dados limpos devem ser colocados em uma pasta `results`.
> 4. Coloque os scripts e os programas em um diretório `src`. Os programas importados de outros locais devem ser alocados no diretório `bin`.
> 5. Escolha nomes que indiquem a função de cada arquivo.
>
{: .callout}

> ## Dica: Modelo de projeto - uma possível solução
>
> Uma maneira de automatizar o gerenciamento de projetos se dá com a instalação do pacote `ProjectTemplate`. Esse  > pacote oferece uma estrutura que é considerada ideal para o bom gerenciamento do projeto. O pacote é útil porque > mostra o fluxo de trabalho de forma organizada e estruturada. Com o RStudio e com o Git é possível ter controle  > total dos trabalhos, além de facilitar o compartilhamento dos arquivos com colaboradores.
>
> 1. Instale o pacote ProjectTemplate
> 2. Carregue o pacote
> 3. Inicie o projeto:
>
> 
> ~~~
> install.packages("ProjectTemplate")
> library("ProjectTemplate")
> create.project("../my_project", merge.strategy = "allow.non.conflict")
> ~~~
> {: .r}
>
> Para mais informações sobre o pacote `ProjectTemplate` e suas funcionalidades acesse   
> [ProjectTemplate](http://projecttemplate.net/index.html)
{: .callout}

### Separe as funções das aplicações

O modo mais efetivo de trabalhar no R é brincando com os códigos na sessão interativa. Quando temos certeza de que os códigos funcionam e fazem o que queremos, copiamos para um arquivo de script. Também é possível salvar todos os comandos utilizados, para isso utilizamos a função *history()*. Utilizar essa função nem sempre é útil pois quando estamos desenvolvendo algum programa novo surgem muitos erros.

Quando o prejeto é novo, geralmente o arquivo de script contém muitas linhas. Quando o projeto está em um estágio mais avançado pedaços de códigos podem ser re-utilizados. É uma boa ideia separar os códigos em diferrentes pastas; Uma para salvar os códigos que serão utilizados com frequência e outra para salvar os scripts das análises feitas.

> ##  Dica: evite duplicação
>
> É possível que o mesmo conjunto de dados e o mesmo script sejam usados em projetos distintos. De modo geral 
> queremos evitar a duplicação de arquivos de modo a salvar espaço e não termos que atualizar o mesmo código em 
> diferentes lugares.

> Quando este for o caso é interessante usar *symbolic links*, que são atalhos para arquivos que se encontram em 
> outro lugares. No Linux e no OS X podemos usar o comando `ln -s`, no Windows podemos criar um atalho ou usar o
> comando `mklink` no terminal de comandos.
{: .callout}


### Salvando os dados na pasta data

Agora que não temos uma boa estrutura para o diretório iremos colocar/salvar os dados na pasta `data/`.

> Faça download dos dados gapminder [aqui](https://raw.githubusercontent.com/resbaz/r-novice-gapminder-files/master/data/gapminder-FiveYearData.csv).
>
> 1. Baixe o arquivo (CTRL + S, right mouse click -> "Save as", or File -> "Save page as")
> 2. Tenha certeza que está salvo com o nome `gapminder-FiveYearData.csv`
> 3. Salve o arquivo na pasta `data/` dentro do seu projeto.
> 
> Iremos carregar e inspecionar esses dados mais tarde.
{: .challenge}

> ## Desafio 2
> É útil ter alguma ideia geral sobre o banco de dados, diretamente pela linha de 
> comando, antes de carregá-los no R. Entendendo o banco de dados bem será útil quando
> formos fazer decisões sobre como carregá-lo no R. Use a linha de comando shell para
> responder as seguintes questões:
> 1. Qual é o tamanho do arquivo?
> 2. Quantas linhas de dados ele contém?
> 3. Quais são os tipos de dados dos valores armazenados neste arquivo?
>
> > ## Solução do exercício 2
> >
> > Rodando os seguintes comandos no shell:
> > 
> > ~~~
> > ls -lh data/gapminder-FiveYearData.csv
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > 
> > ~~~
> > -rw-r--r--  1 gabrielfranco89  staff    80K Mar 22 19:32 data/gapminder-FiveYearData.csv
> > ~~~
> > {: .output}
> > O tamanho do arquivo é 80K.
> > 
> > ~~~
> > wc -l data/gapminder-FiveYearData.csv
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > 
> > ~~~
> >     1705 data/gapminder-FiveYearData.csv
> > ~~~
> > {: .output}
> > Existem 1705 linhas que são parecidas como em:
> > 
> > ~~~
> > head data/gapminder-FiveYearData.csv
> > ~~~
> > {: .r}
> > 
> > 
> > 
> > 
> > ~~~
> > country,year,pop,continent,lifeExp,gdpPercap
> > Afghanistan,1952,8425333,Asia,28.801,779.4453145
> > Afghanistan,1957,9240934,Asia,30.332,820.8530296
> > Afghanistan,1962,10267083,Asia,31.997,853.10071
> > Afghanistan,1967,11537966,Asia,34.02,836.1971382
> > Afghanistan,1972,13079460,Asia,36.088,739.9811058
> > Afghanistan,1977,14880372,Asia,38.438,786.11336
> > Afghanistan,1982,12881816,Asia,39.854,978.0114388
> > Afghanistan,1987,13867957,Asia,40.822,852.3959448
> > Afghanistan,1992,16317921,Asia,41.674,649.3413952
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Dica: linha de comando no R Studio
>
> Você pode rapidamente abrir um shell em RStudio usando o item **Tools -> Shell**  do menu.
{: .callout}

### Controle de versão

Também podemos integrar nosso projeto com git, o colocando sob controle de versão. RStudio possui uma interface para o git melhor que a do shell, mas é bastante limitada no que ela pode fazer, logo você ocasionalmente se encontrará precisando usar o shell. Vamos continuar e fazer um primeiro commit dos nossos templates.

O painel workspace/history tem um botão para Git. Podemos selecionar cada arquivo marcando nas caixas: você verá um "A" verde próximo dos arquivos e pastas, e pontos de interrogações amarelos próximos dos arquivos ou pastas que o git ainda não conhece. RStudio também mostra para você a diferença entre arquivos de diferentes commits.

> ## Dica: Versão para saída descartável
>
> Geralmente você não deseja criar uma versão para saída descartável (ou dados para
> somente leitura). você deve modificar o arquivo `.gitignore` para dizer ao git para
> ignorar esses arquivos e pastas.
{: .callout}

> ## Desafio 3
>
> 1. Crie uma pasta dentro do seu projeto com o nome `graphs`.
> 2. Modifique o aquivo `.gitignore` para conter `graphs` de forma que essa saída
> descartável não seja versionada.
>
> Adicione as novas pastas criadas para o controle de versão usando a interface git.
>
> > ## Solução do exercício 3
> >
> > Isso pode ser feito com as linhas de comando:
> > ```
> > $ mkdir graphs
> > $ echo "graphs/" >> .gitignore
> > ```
> > {: . shell}
> {: .solution}
{: .challenge}
